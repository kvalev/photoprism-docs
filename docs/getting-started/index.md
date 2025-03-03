# Setup

PhotoPrism can be installed on all operating systems supporting [Docker](https://store.docker.com/search?type=edition&offering=community), as well as [FreeBSD](ports/freebsd.md), [Raspberry Pi](raspberry-pi.md), and many [NAS devices](nas/synology.md). It is also available in the cloud on [PikaPods](cloud/pikapods.md) and [DigitalOcean](cloud/digitalocean.md).

We recommend running PhotoPrism with [Docker Compose](docker-compose.md) when hosting it on a private server. It is available for Mac, Linux, and Windows.

Once the initial setup is complete, our [First Steps 👣](../user-guide/first-steps.md) tutorial guides you through the user interface and settings to ensure your library is indexed according to your individual preferences.

!!! tldr ""
    Our [stable version and development preview](https://docs.photoprism.app/release-notes/) have been built into a
    single [multi-arch Docker image](https://link.photoprism.app/docker-hub) for 64-bit AMD, Intel,
    and ARM processors. That means, [Raspberry Pi](raspberry-pi.md) 3 / 4, Apple Silicon, and other ARM64-based
    devices can pull from the same repository, enjoy the exact same functionality, and can follow the regular
    [installation instructions](docker-compose.md) after going through a short list of [requirements](raspberry-pi.md).
    See [FAQs](faq.md) for instructions and notes on [alternative installation methods](faq.md#how-can-i-install-photoprism-without-docker).

## Roadmap ##

Our vision is to provide the most user- and privacy-friendly solution to keep your pictures organized and accessible.
The [roadmap](https://link.photoprism.app/roadmap) shows what tasks are in progress, 
what needs testing, and which features are going to be implemented next.

We have a zero bug policy and do our best to help users when they need support or have other questions.
This comes at a price, as we can't give exact deadlines for new features.

Having said that, funding really has the highest impact. So users can do their part and
[become a sponsor](https://photoprism.app/membership) to get their favorite features as soon as possible.

## System Requirements ##

We recommend hosting PhotoPrism on a server with **at least 2 cores**, **3 GB of physical memory**,[^1] and
a 64-bit operating system. Beyond these minimum requirements, the amount of RAM should [match the number of CPU cores](troubleshooting/performance.md#memory).

If your server has [less than 4 GB of swap space](troubleshooting/docker.md#adding-swap) or a manual
memory/swap limit is set, this can cause unexpected restarts, for example, when the indexer temporarily
needs more memory to process large files. High-resolution panoramic images may require additional swap space
and/or physical memory above the recommended minimum.

!!! note ""
    Indexing large photo and video collections significantly benefits from [local SSD storage](troubleshooting/performance.md#storage)
    and plenty of memory for caching. Especially the conversion of RAW images and the transcoding of videos are very demanding.
    We take no responsibility for instability or performance problems if your device does not meet the requirements.

#### Browsers ####

Our [Progressive Web App](../user-guide/pwa.md) (PWA) works with most modern browsers, and runs best on [Chrome](https://www.google.com/chrome/), [Chromium](https://www.chromium.org/getting-involved/download-chromium), [Safari](https://www.apple.com/safari/), [Firefox](https://www.mozilla.org/en-US/firefox/all/#product-desktop-release), and [Edge](https://www.microsoft.com/en-us/edge).
You can conveniently install it on the home screen of all major operating systems and mobile devices.

Please note that not all [video and audio formats](https://caniuse.com/?search=video%20format) can be [played with every browser](troubleshooting/browsers.md). For example, [AAC](https://caniuse.com/aac "Advanced Audio Coding") - the default audio codec for [MPEG-4 AVC / H.264](https://caniuse.com/avc "Advanced Video Coding") - is supported natively in Chrome, Safari, and Edge, while it is only optionally supported by the OS in Firefox and Opera.

#### Databases ####

The backend is compatible with [SQLite 3](https://www.sqlite.org/) and [MariaDB](https://mariadb.org/) 10.5.12+.[^2] Support for MySQL 8 has been discontinued due to low demand and missing features.[^3]

#### External Services ####

As explained in detail in our [Privacy Policy](https://photoprism.app/privacy), reverse geocoding and interactive world maps depend on the necessary data being [retrieved from us](https://photoprism.app/contact) and [MapTiler AG](https://www.maptiler.com/contacts/), headquartered in Switzerland. Both services require an Internet connection if you want to use them.[^4]

#### HTTPS ####

If you install PhotoPrism on a public server outside your home network, **always run it behind a secure HTTPS reverse proxy** such as [Traefik](proxies/traefik.md) or [Caddy](proxies/caddy-2.md).
Your files and passwords will otherwise be transmitted in clear text and can be intercepted by anyone, 
including your provider, hackers, and governments. Backup tools and file sync apps like [FolderSync](https://www.tacit.dk/foldersync/faq/#i-can-not-connect-to-a-non-https-webdav-server-why) 
may refuse to connect as well.

## Getting Support ##

If you need help installing our software at home, you can [join us on Reddit](https://link.photoprism.app/reddit), ask in our [Community Chat](https://link.photoprism.app/chat), or post your question in [GitHub Discussions](https://link.photoprism.app/discussions). Common problems can be quickly diagnosed and solved using our [Troubleshooting Checklists](https://docs.photoprism.app/getting-started/troubleshooting/).

We'll do our best to answer all your questions. In return, we ask you to [back us](https://photoprism.app/membership) on [Patreon](https://link.photoprism.app/patreon) or [GitHub Sponsors](https://link.photoprism.app/sponsors).
Think of "free software" as in "free speech," not as in "free beer". Thank you!

In exchange for their continued support, [sponsors](https://photoprism.app/membership) are also welcome to request direct technical [support via email](mailto:sponsors@photoprism.app). Please bear with us if we are unable to get back to you immediately due to the high volume of emails and contact requests we receive.

!!! info ""
    **We kindly ask you not to report bugs via *GitHub Issues* unless you are certain to have found a fully reproducible and previously unreported issue that must be fixed directly in the app.**
    [Contact us](https://photoprism.app/contact) or [a community member](https://link.photoprism.app/discussions)
    if you need help, it could be a local configuration problem, or a misunderstanding in how the software works.

[^1]: RAW image conversion and TensorFlow are disabled on systems with 1 GB or less memory
[^2]: Our [`docker-compose.yml` examples](https://dl.photoprism.app/docker/docker-compose.yml) are generally based on the latest [MariaDB Server](https://mariadb.com/kb/en/mariadb-server-release-dates/) release to take advantage of performance enhancements. That doesn't mean older versions are no longer supported.
[^3]: Oracle seems to have stopped shipping [new features and enhancements](https://github.com/photoprism/photoprism/issues/1764). As a result, the testing effort required before each release is no longer feasible.
[^4]: Please make sure that you allow these requests if you have a firewall installed and verify that your Internet connection is working. See also "Privacy and Security" in our [Compliance FAQ](https://photoprism.app/kb/compliance-faq#privacy).