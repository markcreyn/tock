tock
===============

We use Tock to track our time. You can read more about Tock in this [blog post](https://18f.gsa.gov/2015/05/21/tockingtime/) about its features.

[![Build Status](https://travis-ci.org/18F/tock.svg)](https://travis-ci.org/18F/tock)

![Screenshot of Tock](https://18f.gsa.gov/assets/blog/tockingtime/tock03.jpg)

## Getting Started

Make sure you have `vagrant` installed. For instance, on OS X with Homebrew:

```
$ brew install caskroom/cask/brew-cask
$ brew cask install vagrant
```

Then, ensure you have the appropriate Vagrant Box installed:

```
$ vagrant box add ubuntu/trusty32
```

You can get started with development by running the `Vagrantfile`:

```
$ vagrant up
```

This will provision an entire setup for you pretty quickly (see `provision/dev/bootstrap.sh`). You can access Django and start `runserver` by doing the following:

```
$ vagrant ssh
$ python manage.py migrate
$ python manage.py loaddata test_data/data-update.json  
$ python manage.py runserver
```

From your host computer, going to http://192.168.33.10 will enable you to view Tock. You're automatically logged in as `testuser@gsa.gov`, the nginx proxy in production will pull the logged in user from Google Auth proxy. You can access the admin panel at http://192.168.33.10/admin

### Making SASS changes

In order to make official changes to the styling of the website, you'll need to compile locally and submit the files accordingly. All of the files you should be editing are located in `tock/tock/static/sass/` and are labeled according to their purpose, e.g. `base/_typography.scss` focuses on website type stylings.

Here are some steps to do to help make that happen:

1. Make sure that you have Sass installed on your machine, [instructions for installing Sass on various platforms.](http://sass-lang.com/install)
2. Open a new terminal window, separate from the one running the vagrant instance described above.
3. Type the following command from the top level `tock` directory:

```
$ sass --watch tock/tock/static/sass/core.scss:tock/tock/static/css/style.css
```

Congrats! Now you'll be able to make the changes and they will compile automatically every time your changes are saved.

**NOTE: Be sure to ONLY change files ending in  `.scss` extension and NOT `.css`**

## API

Tock has an API, you can get the full dataset with:  https://tock.18f.gov/api/timecards_bulk.csv
or page thru results with: https://tock.18f.gov/api/timecards.json
you can choose a different page or page size: https://tock.18f.gov/api/timecards.json?page=2&page_size=100
