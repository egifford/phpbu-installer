# phpbu-installer

Helper scripts for installing and running PHPBU.

PHPBU is a php framework that creates and encrypts backups, syncs your backups to other servers or cloud services and
assists you monitor your backup creation.

Read more about PHPBU:

* https://phpbu.de/
* https://github.com/sebastianfeldmann/phpbu

## What is this project and how is it different from PHPBU?

This project provides two addons to PHPBU:

* A preconfigured composer.json file which includes PHPBU and the SDK for AWS, which allows PHPBU to upload backups to S3.
* A launching script which gives you control over which PHP executable runs PHPBU and a way to override settings from php.ini.   

## Installation Steps

### Prerequisites

1. This installation procedure requires the tools listed below.  Ensure that they are installed first.
    * Git
    * Composer
2. There are some recommended environmental configuration settings.  These installation steps will assume the Bash
environment and give steps for altering .bashrc.  See the **PHP Configuration** section.

### PHP Configuration

To control which PHP executable is used to run PHPBU, add the following to the .bashrc file for any user that needs to
run PHPBU:
	
`export PHPBU_PHP=/path/to/php/executable`
	
PHPBU may require some php.ini settings to be overridden on the command line.  By default, this project executes PHP
with `allow_url_fopen=1`.  If other PHP settings need to overridden, override settings can be added to .bashrc:
	
`export PHPBU_PHP_OPTIONS="-d allow_url_fopen=1 -d OTHERSETTING -d SOME_OTHER_SETTING"`

Follow the pattern shown above.  Each overridden setting must be preceded by `-d`.  Please always include
`-d allow_url_fopen=1`.

After making changes to .bashrc, you will need to logout and login to have them  take effect.  Alternatively, run the
following:
	
`source ~/.bashrc`
	
### Installation

1. Create a directory for the installation.
2. Move into the new directory.
3. Use Git to pull down the PHPBU project:

    `git init`

    `git remote add origin https://github.com/egifford/phpbu-installer.git`

    `git pull origin master`

4. The master branch contains the latest, bleeding edge of this project.  If a particular version is desired, use the
following command, but type a versioned tag instead of the text "VERSION-TAG":
    * `git checkout VERSION-TAG`
    * To list what versions are available, use: `git tag`
5. Install PHP code: `composer update --no-dev -o`
6. Make the PHPBU script executable: `chmod 755 phpbu`
7. Test the installation: `./phpbu --version`
8. You should see about like: `phpbu 4.0.10`
