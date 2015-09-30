# Developer Onboarding Guide
Welcome to Tada! We're happy you're here. Let's get started.

This guide has one goal: **Check code into production by the end of the day.**

## Dev Machine Setup

* [Package Management](#package-management)
* [Terminal Setup](#terminal-setup)
* [Browser Setup](#browser-setup)
* [Communication](#communication)
* [Credential Management](#credential-management)
* [Editor and Plugins](#editor-and-plugins)
* [Dev Environment](#dev-environment)
* [Source Control](#source-control)
* [Production Tools](#production-tools)

If you get stuck, as for help in [team chat](https://tadaworks.slack.com).

A word of advice: Don't get hung up on the breadth of any new tech. It'll all make sense soon, and Google is your friend until then.

## Package Management

[Homebrew](http://brew.sh) is the "missing package manager for OS X", and makes keeping bits in sync way easier.

Open your terminal and run the following commands:

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
```

While you're at it, install [cask](http://caskroom.io), which extends what can be installed from homebrew.

```bash
brew install caskroom/cask/brew-cask
```

## Terminal Setup

The default terminal that you've been using **works**, but once you go [iTerm2](https://www.iterm2.com) + [Zsh](http://ohmyz.sh), you never go back.

```bash
brew cask install iterm2
```

You can install Zsh from the terminal. There's a good chance that it's going to fail on your first run, and you'll be prompted to install Apple deverloper tools. After installing those, run the command again.

```bash
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

Looking for `alt + ←` or `cmd + →`? Yeah, us too. [This thread on StackOverflow](http://stackoverflow.com/questions/6205157/iterm2-how-to-get-jump-to-beginning-end-of-line-in-bash-shell) provides a fix.

Zsh has a ton of [plugins](https://github.com/robbyrussell/oh-my-zsh/tree/master/plugins) available for tab-based auto complete, which can be activated by adding entries to the `plugins` tuple in `~/.zshrc`. Here are a few that we use:

```bash
plugins=(git aws brew github heroku npm node osx vagrant)
```

Looking for a theme? Lots of people love [Solarized](http://ethanschoonover.com/solarized), and [Dracula](http://zenorocha.github.io/dracula-theme/iterm) is a favorite of ours. 

## Browser Setup

We use Chrome, Firefox, and Safari (you're probably looking at it) regularly for sanity-checking compatability.

```bash
brew cask install google-chrome
brew cask install firefox
```

### Plugins
* [React Developer Tools](https://github.com/facebook/react-devtools) | [Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi) | [Firefox](https://addons.mozilla.org/firefox/addon/react-devtools/): Makes developing [React](https://github.com/facebook/react) views easier.
* [Postman](https://www.getpostman.com/) | [Chrome](https://chrome.google.com/webstore/detail/postman-rest-client/fhbjgbiflinjbdggehcddcbncdddomop): HTTP and REST client for testing APIs

### Wait, what about IE?

We have a collection of Windows VMs to test the app in markets where legacy support is a must. These installs are outside of the scope of this guide, so ask for help if you're working on a market-sensitive feature.

## Communication
We prize strong communication. Bookmark these links as you'll be referring to them often.

[Tada @ Slack](https://tadaworks.slack.com): Team chat
[Tada Dev @ Trello](https://trello.com/tadadev/): Sprint planning boards

## Credential Management
[Lastpass](https://lastpass.com) is used for securely sharing credentials, certificates, and other things too sensitive to pass around by email.

You can [install Lastpass here](https://lastpass.com/download/cdn/lpmacosx.zip). This is extremely sensivite software, and the preferred install method is via this link.

If you feel really adamant about managing this install from Homebrew, just make sure that `brew cask info lastpass` references `https://github.com/caskroom/homebrew-cask/blob/master/Casks/lastpass.rb`, and that `lastpass.rb` points to `https://lastpass.com/download/cdn/lpmacosx.zip`.

### But I Love 1Password!
Us too, but LastPass lets us federate and log access, which beats passing around a keystore. Your creds will arrive on edible paper shortly.

## Editor and Plugins
Yes, you can use your favorite editor.

We use [Sublime](http://www.sublimetext.com/). This setup works with all of our stuff, so if you aren't super opinionated, give it a spin. Even if you are, you should probably follow along since your editor needs to support equivalent plugins.

```bash
brew cask install caskroom/versions/sublime-text3
```

Next, run this command to allow you to call sublime from the terminal

```bash
sudo ln -s /Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl /usr/bin/sublime
```

###Plugins

[Install Package Control](https://packagecontrol.io/installation), which manages plugins within ST.

`Cmd + shift + p` opens the Package Control prompt after installation. Search `install` and select `Package Control - Install Package` for each of the following:

* [Babel](https://github.com/babel/babel-sublime)
* [Editor Config](https://github.com/sindresorhus/editorconfig-sublime#readme)
* [Sass](https://github.com/P233/Syntax-highlighting-for-Sass "For syntax highlighting")
* [Sublime Linter](http://sublimelinter.readthedocs.org/en/latest/installation.html)
* [SublimeLinter-eslint](https://github.com/roadhump/SublimeLinter-eslint)
  * Run: `brew install node`
  * Run: `npm install -g eslint`
* [SublimeLinter-scss-lint](https://github.com/attenzione/SublimeLinter-scss-lint)
  * Run: `npm install -g sass-lint`
* [Markdown Preview](https://github.com/revolunet/sublimetext-markdown-preview)

You can also install themes like [Solarized](http://ethanschoonover.com/solarized) and [Dracula](https://github.com/zenorocha/dracula-theme#sublime-text) (along with thousands of others) in Package Control.

##Dev Environment
We host our development environments in [VirtualBox](https://virtualbox.org) VMs, managed using [Vagrant](https://vagrantup.com). This helps us eliminate random per-machine config isues when bugs crop up, and improves reproducability.

```bash
brew cask install virtualbox
brew cask install vagrant
```
###Where's Otto?
It's under investigation, and will likely find its way into our stack if we decide to migrate away from Heroku.

##Source Control
We use [Git](https://git-scm.com) for source control, and [GitHub](https://github.com) as our host.

If you don't already have one, [create a GitHub account](https://github.com/join) and then [follow this guide](https://help.github.com/articles/generating-ssh-keys) to generate an [SSH](https://en.wikipedia.org/wiki/Secure_Shell) key and test GitHub authentication.

Get someone official looking to add you to the [Tada Works](https://github.com/tadaworks) organization so you can start pulling down code!

### New to Git?
We've all been there. Here's an excellent tutorial](https://try.github.io/levels/1/challenges/1)

[Git from the Bottom Up](https://jwiegley.github.io/git-from-the-bottom-up) is another fantastic resource to help you think about how Git works, something most people who use it every day don't fully understand. We recommend this even to seasoned folk.

## Production Tools
We currently deploy to a mix of [Firebase](https://firebase.com), [Heroku](https://heroku.com), and [AWS](https://aws.amazon.com) services. Credentials for each service are available in LastPass.

	```bash
	brew install heroku-toolbelt
	brew install awscli
	brew cask install java
	brew cask install dynamodb-local
	```

### Getting Familiar
[Babel Try Out](https://babeljs.io/repl): Babel is an [ES2015 (aka ES6)](https://github.com/lukehoban/es6features) to vanilla JavaScript transpiler, allowing us to write modern JavaScript code today.
[Firebase Tutorial](https://www.firebase.com/tutorial/#gettingstarted): A 5-minute tutorial to get acquainted with Firebase and its features. It powers the real-time part of our stack.
[Heroku Node Tutorial](https://devcenter.heroku.com/articles/getting-started-with-nodejs#introduction): A quick getting started guide for building and launching Node.js apps on Heroku.
[A Beginner's Guide to NPM](http://www.sitepoint.com/beginners-guide-node-package-manager): A quick overview of the [Node Package Manager]https://www.npmjs.com/
[Webpack Tutorial](http://webpack.github.io/docs/tutorials/getting-started/): Gives an overview of the Webpack module bundler, a tool we use to package up our JavaScript code for the web.

## On the Way Out

This is a pretty brief overivew, designed to get you up and running as quickly as possible. If you have any questions, ask them in team chat. A great one to start with: **"Hey, why are we using JavaScript?"**


