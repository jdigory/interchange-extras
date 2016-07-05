# Run Interchange under Plack

This may not be the fastest way to run Interchange, but if you need a
quick-and-dirty local development instance, it can't be beat.

To run this in production, you'll probably want to proxy it with Nginx,
and you should have a startup/shutdown script for `plackup`, perhaps
with [Ubic](https://metacpan.org/pod/Ubic).

## Setup

First, you'll need `cpanm`:
`% curl -L https://cpanmin.us | perl - App::cpanminus`

Then Plack and a few middlewares:

```
cpanm Plack Plack::Builder Plack::App::WrapCGI Plack::Middleware::Static Plack::Middleware::ForceEnv
```

## Configuration

Copy the [psgi file](app.psgi) to your Interchange root:
`cp app.psgi /path/to/interchange/`
and customize it.

Customize your catalog's `products/variable.txt` or copy
[`products/site.txt`](site.txt) to your catalog and adjust the
variables within.

Set `Mall No` in your `interchange.cfg`.

## Start

`plackup -s Starman --workers=1 -p 5001 -a /path/to/interchange/app.psgi -D`

## Load

http://localhost:5001/

## Extra credit: expose your local server to the internet

Install [ngrok](https://ngrok.com/) and run with `ngrok http 5001`.
Alter the server variables in `site.txt` to use the provided hostname,
and restart or reconfigure Interchange.

Share with friends, clients, or coworkers.