# Comments on Provision Vagrant with Ansible homework

### Part one

In a real world thing, we might need to enable
some older TLS protocols, depending on who our customers were (the general
public might not all be on the latest/greatest browsers, but technical users
probably could be assumed to be able to get up to date).

The ciphers probably could be shortened to just HIGH, which _ought_ to
always be the most recommended ciphers, but I found somebody who thought
it was better to enumerate them.  This is fine, but more importantly,
we need to make sure that these are easy and safe to upgrade, because
the state of the art is always advancing.

If I had designed this, I might have made the config file not be clearly
aimed at replacing nginx.conf, but instead made it more appropriate for
placing in /etc/nginx/conf.d, since that lets the base nginx.conf upgrade
with the package, possibly getting more secure config or better logging,
and lets us just focus on the app stuff that we want.

### Part two

I chose to upgrade all packages at the start, which is good for security,
but slow.  If this were deployed in a real environment, we'd probably have
a process to create an image with CI to use so that this step would be very
short.

The packagecloud repo seems a bit sketchy, but hey, it's centos 6.8, and I
guess this is where you get this stuff.  :-)  At least we have some gpg
checking and so on for the repo.

I would have set up logging for the app, but it appears as if the app
redirects everything to /dev/null anyways, so to keep things simple, I did
not , though it would definitely be the next thing I would do,
along with NTP (to have correlatable logs with other systems) and some
off-box centralized logging thing.

