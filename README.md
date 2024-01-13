
# Overleaf Toolkit

This repository contains the Overleaf Toolkit, the standard tools for running a local
instance of [Overleaf](https://overleaf.com). This toolkit will help you to set up and administer both Overleaf Community Edition (free to use, and community supported), and Overleaf Server Pro (commercial, with professional support).

The [Developer wiki](https://github.com/overleaf/overleaf/wiki) contains further documentation on releases, features and other configuration elements.


## Getting Started

Clone this repository locally:

``` sh
git clone https://github.com/overleaf/toolkit.git ./overleaf-toolkit
```

For the official instruction follow the [Quick Start Guide](./doc/quick-start-guide.md).

## Installation
This guide should help you set up Overleaf on your server with the specified version numbers for ShareLaTeX and the Docker image. Adjust version numbers and configurations as needed.

1. **Clone this repository locally:**

```bash
sudo apt install docker docker-compose lsb-release libxml-libxslt-perl
git clone https://github.com/overleaf/toolkit.git ./overleaf-toolkit
cd overleaf-toolkit
bin/init
```

2. **Change the version number of ShareLaTeX and the Docker image:**

```bash
nano config/version
```
Change the version numbers as needed (I used 4.1.1).

3. **Build and run Overleaf using Docker Compose:**

```bash
sudo bin/up
```
This command may take some time. You can leave it running and open a new terminal for the next steps.

4. **Configure the ShareLaTeX container:**

In a new terminal, run the following commands:

```bash
sudo bin/shell sharelatex
apt-get update
apt install -y context libxml-libxslt-perl cpanminus
rm -rf /var/lib/apt/lists/*
tlmgr update --self
tlmgr install revtex amsmath textcase listings fncychap biblatex cancel pdfpages setspace footmisc bigfoot multirow lettrine minifp textpos subfig caption placeins epigraph pdflscape ec cm-super biber biblatex times bibtex collection-latexrecommended collection-latexextra collection-bibtexextra collection-fontsrecommended
tlmgr install collection-mathscience
tlmgr install collection-pstricks
tlmgr install collection-fontutils
tlmgr install collection-fontsextra
tlmgr install collection-binextra
tlmgr install xetex
mtxrun --generate
mktexlsr
updmap-sys
fmtutil-sys --all
tlmgr install scheme-full
tlmgr path add
cd /home
wget https://github.com/plk/biber/archive/refs/tags/v2.19.zip 
unzip v2.19.zip 
cd biber-2.19/
cpan
> install Module::Build
> install PAR::Packer
> quit
perl ./Build.PL
./Build installdeps
ldconfig
./Build test 
./Build install
tlmgr path add
```

5. **Restart the other terminal:**

Press `CTRL+C` to stop the previous command (`/bin/up`) in first terminal and re-run it:

```bash
sudo bin/up
```

6. **Creating and managing users:**

Once the Overleaf instance is running, visit the `/launchpad` page to set up your first admin user. For further documentation visit [here](https://github.com/overleaf/overleaf/wiki/Creating-and-managing-users).

## Documentation

See [Documentation Index](./doc/README.md)


## Contributing

See the [CONTRIBUTING](https://github.com/overleaf/overleaf/blob/main/CONTRIBUTING.md) file.


## Getting Help

Users of the free Community Edition should [open an issue on github](https://github.com/overleaf/toolkit/issues). 

Users of Server Pro should contact `support@overleaf.com` for assistance.

In both cases, it is a good idea to include the output of the `bin/doctor` script in your message.

