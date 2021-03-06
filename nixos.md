# Pros and cons of NixOS

I've experimented with many operating systems over the years. Even
though I became an [OpenBSD](https://www.openbsd.org/) loyalist in the
end, [NixOS](https://www.openbsd.org/) was my daily driver for some
time. There are a lot of upsides to NixOS, and some downsides. Let's
take a moment to understand NixOS before we dive into the pros and cons.

## What's NixOS like?

Where many Linux distributions share a number of fundamental
similarities (certainly, they don't differ as much as the BSDs), NixOS
is substantially different.

One of the most important concepts to understand is that NixOS is mostly
modified by editing a central configuration file. What do I mean by
this?

Under the imperative paradigm of system management, the OpenSSH daemon
is enabled like so (using Debian as an example).

1. Install OpenSSH.

		# apt install openssh-server

1. Enable the OpenSSH daemon.

		# systemctl enable ssh

Contrast this with a declarative system like NixOS.

1. Modify `/etc/nixos/configuration.nix` so NixOS knows to enable the
   OpenSSH daemon.

		services.sshd.enable = true;

1. Rebuild and switch to the new configuration.

		# nixos-rebuild switch

This installs OpenSSH if it's not already present on the system and sets
it up. Maintaining a NixOS installation is an ongoing process of
describing and subsequently rebuilding a system.

As a result of what it sets out to do, NixOS doesn't follow the
Filesystem Hierarchy Standard. Most things are isolated from one another
in `/nix/store`.

## Pros

### Consistency

Managing a system declaratively is more consistent and reproducible. It
feels like every program's configuration files use a different syntax,
and NixOS offers the opportunity to configure everything with one
language: Nix. When I realized this meant I could configure fonts
without XML, I was sold. It's the difference between this:

	<?xml version='1.0'?>
	<!DOCTYPE fontconfig SYSTEM 'fonts.dtd'>
	<fontconfig>
		<alias>
			<family>serif</family>
			<prefer>
				<family>Noto Serif</family>
			</prefer>
		</alias>
		<alias>
			<family>sans-serif</family>
			<prefer>
				<family>Noto Sans</family>
			</prefer>
		</alias>
		<alias>
			<family>monospace</family>
			<prefer>
				<family>Noto Mono</family>
			</prefer>
		</alias>
	</fontconfig>

And this:

	fonts.fontconfig.defaultFonts = {
		serif = [ "Noto Serif" ];
		sansSerif = [ "Noto Sans" ];
		monospace = [ "Noto Mono" ];
	};

I'd rather write the second one.

### Reliability

Rollbacks and atomic upgrades are a part of NixOS as well. If one
version of the system doesn't boot, booting into the last working
configuration is easy enough to do (assuming the problem isn't related
to the boot loader).

### Aids in development

Probably one of the most killer features for developers is
[`nix-shell`](https://nixos.org/manual/nix/stable/#sec-nix-shell).
Temporary, reproducible environments can be created with whatever
packages are needed. Once `nix-shell` is exited, those packages are no
longer in PATH. While virtual environments aren't exclusive to NixOS,
it's convenient to have a language agnostic tool for this included with
the system. `nix-shell` is more or less limited to the imagination
given that it uses the Nix language.

### Self-documenting

NixOS is self-documenting in a certain light. System configuration
happens in one place, `/etc/nixos`. Since maintaining a NixOS
installation is an ongoing process of describing the desired system state,
`/etc/nixos` is a living, breathing record of the changes made. Because
of its reproducible nature, NixOS is a great choice for server farms.

### Custom ISOs are a cinch

One last pro: creating a live ISO to a set of specifications by
leveraging Nix is much more pleasant than doing it imperatively in my
experience. It's easier to understand what the live system does because
its internals are laid bare in the configuration file. The ISO also
won't build if there's a problem.

Declarative configuration is visionary in some respects and in
principle, I like it a lot. [So why did I switch to
OpenBSD](/why-openbsd.html)?

## Cons

### NixOS isn't simple

Many of the problems NixOS suffers are upstream problems (problems with
Linux in general). I like systems that abide by the KISS philosophy and
simplicity is an area Linux, and by extension NixOS, often doesn't do as
well in.

For instance, compare the tool NixOS uses to manage services,
[`systemctl(1)`](https://www.mankier.com/1/systemctl), with OpenBSD's
[`rcctl(8)`](https://man.openbsd.org/rcctl). Other examples include the
sound server (pulseaudio versus sndio), method of privilege elevation
(sudo versus doas), firewall (iptables versus pf), and so on.

In comparing these pieces of software, I'm illustrating a point:
additional features aren't unequivocally good. Sometimes features are
useful and other times they're unneeded or poorly implemented. For this
reason, lacking unnecessary features *is* a feature.

### Managing things declaratively is sometimes harder

NixOS presents a completely different approach to system management and
while powerful, it can also be frustrating. When the magic behind the
scenes stops working, it can get ugly. To the point that while
abstracting away things in Nix saves effort in some ways, it creates
more work in others.

### No 'secure by default' philosophy

There isn't a focus on security by default in NixOS to the extent that
it exists with OpenBSD. As a sysadmin and someone who's a bit paranoid
(just because I'm paranoid doesn't mean they aren't out to get me),
I need my system to have secure defaults.

Security is often eschewed in favor of new features because the
reward for good security is 'nothing.' No intrusions happen, no damage
is sustained, and no services go down. In other words, the benefit of
good security is often more about what doesn't happen rather than what
does.

## Verdict

Overall, while I enjoy how innovative NixOS is and concede that it has
its advantages, OpenBSD is near and dear to my heart. Sometimes
[`less(1)`](https://man.openbsd.org/less) is
[`more(1)`](https://man.openbsd.org/more).
