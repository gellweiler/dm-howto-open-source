How to Open Source at dm-drogerie markt
==================

A guide to releasing an open-source project at [dm-drogerie markt](https://www.dm.de>), Europe's largest drugstore. Please feel free to use this as a template for your own organization's open source planning, policymaking, and development efforts. If there's a topic we've missed, or if you have any suggestions for making this better, let us know via our Issues tracker.

This is based on Zalando's brilliant '[how to open source](https://github.com/zalando/zalando-howto-open-source)'.


Table of Contents
------------------------------------------------------------
  * [Why Open Source?](#why-open-source-)
  * [Our Open Source Principles](#our-open-source-principles)
  * [Project Design](#project-design)
    + [What to Ask (and Answer) Before You Open Source](#what-to-ask--and-answer--before-you-open-source)
    + [Never Open-Source These:](#never-open-source-these-)
  * [Our public GitHub org site, and internal Bitbucket](#our-public-github-org-site--and-internal-bitbucket)
    + [The Main Org Site and What Makes a Project “Open Source”](#the-main-org-site-and-what-makes-a-project--open-source-)
    + [New Projects: The Incubator](#new-projects--the-incubator)
        * [What happens if I release a project directly to the public GitHub org site?](#what-happens-if-i-release-a-project-directly-to-the-public-github-org-site-)
    + [InnerSource: For dm-internal shared projects](#innersource--for-dm-internal-shared-projects)
- [Project Basics](#project-basics)
  * [Code Review](#code-review)
  * [Creating a README](#creating-a-readme)
    + [Do:](#do-)
    + [Don't:](#don-t-)
    + [Syntax and Formatting](#syntax-and-formatting)
  * [Official Namespace](#official-namespace)
  * [Applying Changes](#applying-changes)
  * [Versioning](#versioning)
  * [Can I Use My Private GitHub Account To Contribute?](#can-i-use-my-private-github-account-to-contribute)
  * [Maintainers](#maintainers)
    + [Create a Maintainers File](#create-a-maintainers-file)
    + [Be Prompt and Responsive](#be-prompt-and-responsive)
    + [Use Issues Creatively](#use-issues-creatively)
  * [Stay Secure](#stay-secure)
      - [Two-Factor Authentication Is Required](#two-factor-authentication-is-required)
  * [About Licensing](#about-licensing)
    + [Quick FAQ](#quick-faq)
      - [Which license do we use?](#which-license-do-we-use-)
      - [Must I use MIT?](#must-i-use-mit-)
      - [I don't like MIT. Can I use another license?](#i-don-t-like-mit-can-i-use-another-license-)
      - [What if I fork an external project and/or contribute to it?](#what-if-i-fork-an-external-project-and-or-contribute-to-it-)
      - [I'm open-sourcing a library. What should I do?](#i-m-open-sourcing-a-library-what-should-i-do-)
      - [What if my team uses an external project whose license is not dm-recommended?](#what-if-my-team-uses-an-external-project-whose-license-is-not-dm-recommended-)
      - [Who is the license owner?](#who-is-the-license-owner-)
      - [Does my project need a LICENSE file?](#does-my-project-need-a-license-file-)
      - [Do I need to add a license header to every source file?](#do-i-need-to-add-a-license-header-to-every-source-file-)
      - [I still have licensing questions. What can I do?](#i-still-have-licensing-questions-what-can-i-do-)
    + [Repository of Meta Information](#repository-of-meta-information)
    + [Restrictions Imposed by the License](#restrictions-imposed-by-the-license)
  * [Other Repository Information](#other-repository-information)
    + [JVM Artifacts](#jvm-artifacts)
    + [Node Modules](#node-modules)
    + [Docker Images](#docker-images)
  * [Working with External Contributors](#working-with-external-contributors)
  * [Project Promotion](#project-promotion)
    + [Proactively Communicate](#proactively-communicate)
  * [Contributing to Non-dm Open-Source Projects](#contributing-to-non-dm-open-source-projects)
      - [CLAs](#clas)




### Why Open Source?

Because it can: improve quality, mitigate risk, increase trust, save us money, expand our technology choices, be fun, enable us to give back to the community, strengthen our tech brand, and attract talent.

Open source software is the base of most of our systems and projects, and supporting it improves ourselves as well as the world around us.
 
### Our Open Source Principles

- **Take Ownership**: Your team is responsible for ensuring that it’s possible to open-source your project. The Open Source Guild and Architecture Guild are available for guidance.
- **Be Safe**: To ensure the broadest possible use of your project, use the MIT license only.
- **Deliver Quality**: Provide a great out-of-the-box experience.
- **Provide Documentation**: Include a clear README and default working configuration.
- **Stay Secure**: Make sure your project doesn’t include dm specifics, such as credentials and private identifiers.
- **Ask for Help**: Find colleagues to brainstorm ideas for your project and to review your work.
- **Promote**: Tell the world about your project via blog posts, social media and conference talks.
- **Join the Open Source Guild**: Help us make Open Source stronger at dm! Come on, it'll be fun. :)


### Project Design

#### What to Ask (and Answer) Before You Open Source

[Danese Cooper](https://twitter.com/DivaDanese) and [Duane O'Brien](https://twitter.com/DuaneOBrien) at PayPal have [shared a succinct four-question approach](https://opensource.com/business/16/1/4-questions-ask-open-sourcing-project) that has influenced our own:

- Who cares?
- Are we still using it?
- Are we committed to it?
- Can it be developed in one public tree?

To dive deeper on the first point, please consider [this product template/checklist](https://github.com/dm-drogeriemarkt/dm-howto-open-source/blob/master/producttemplate.md). It's meant to raise the key questions necessary for a project to reflect a strong "product mindset" and maximum project utility for the community at large.

#### Never Open-Source These:

- Customer data
- Configuration
- Domain knowledge
- Unique Selling Points (USPs)
- Anything that would risk our competitive advantage. This typically means technologies we build that are intrinsic to generating or reinforcing the uniqueness of our customer experience, and that—if made public—would enable our competitors to implement it and erase our uniqueness. This could be:
  - confidential source code
  - recommendation algorithms

If you're open-sourcing a project that has contained sensitive information in the past, the sensitive information can still be retrieved from the Git commit history. Create an entirely new Git repo for it before pushing it to GitHub.

No issues? Great! On to the next section ...

### Our public GitHub org site, and internal Bitbucket

Based on quality, usefulness and maintenance considerations, we use this matrix to decide how to classify and place our projects:

- InnerSource = internal Bitbucket in no specific place or structure
- Open source preparation = internal Bitbucket -> 'Open Source Incubator' project
- Open source = public GitHub org site

The next sections offer more details on differences between open source, “coding in the open” and InnerSource. -> **TODO** Haben wir diese Unterscheidung zwischen coding in the open und Open Source? 

#### The Main Org Site and What Makes a Project “Open Source”

dm's main GitHub organization is [/dm-drogeriemarkt](https://github.com/dm-drogeriemarkt). This organization is reserved for projects meeting these criteria:

- **is useful beyond dm**. It is free of dm dependencies and simple for a user outside dm to install and start using.
- **has user-friendly documentation** that is up-to-date and clear about what the project does, and how to install/start/configure/run it. ([This template can help you](https://github.com/dm-drogeriemarkt/dm-howto-open-source/blob/master/READMEtemplate.md).)
- **is tested**. It has automated tests and takes advantage of test coverage.
- **is under active development**, or is stable enough to be considered a “finished” product. If the project is incomplete, at least one maintainer has worked on it in the last three months. If it’s stable and doesn’t require constant maintenance, you’ve stated as much in your README.
- **is innovative**. If it duplicates an existing project, it does at least one thing better, faster, differently, etc., or is higher-quality.
- **meets our non-negotiable guidelines** regarding security and compliance. 
- **is an MVP**. It either meets or surpasses “minimum viable product” status. An outside developer could use it and even contribute to it. If it’s buggy or very early-stage, it includes a brief development status in the intro stating as much. Maybe the Open Source Incubator is a better place at the moment.
- **has a plan**. Its maintainers care about making it a success. They commit to responding to PRs and issues in a timely manner (48-72 hours), thank contributors, and convert quality contributors to trusted maintainers as appropriate. If you need some guidance, check out [Mozilla's helpful resources](https://mozilla.github.io/open-leadership-training-series/articles/open-project-maintenance/open-project-maintenance/) on this topic.


#### New Projects: The Incubator

The internal Bitbucket project "Open Source Incubator" is most likely where your project will first appear before making it public. It is a proving ground for brand-new projects that don't yet meet all the above criteria. It is where we can experiment and publish projects that show clear promise of being useful to others because they are A) out-of-the-box usable to non-dm users and B) highlight a compelling technical challenge that we are solving with software.
 
All projects now must remain in the Incubator until they meet the basic open source criteria listed in the previous section.


###### What happens if I release a project directly to the public GitHub org site?

Please don't. 

You will be asked to delete the project yourself, and publish it in the Bitbucket Open Source Incubator. If we don’t get any response within seven days, or if you agree to the transfer but don’t take action within seven days, your project will be deleted.


#### InnerSource: For dm-internal shared projects
InnerSource projects are the repositories we use internally at dm, or which do not yet meet our criteria for open source. They appear on Bitbucket, and are not accessible to the public. No one outside of dm can see or contribute to them. 

Right now there is no specific Bitbucket project for these repos.


**Wait, shouldn't we open-source everything in future? Isn’t keeping repos on Bitbucket the wrong way?**

Nope. Not every project we create will be appropriate for sharing publicly. Some projects will be [too sensitive for publication](https://github.com/dm-drogeriemarkt/dm-howto-open-source#never-open-source-these). Other projects would act as “noise,” because they are too tightly coupled to what we do internally. An organization's open source footprint says a lot about that organization, especially if the org cannot maintain a good signal-to-noise ratio.

However, we still want you to share these projects inside dm. This is why we advocate the InnerSource collaboration model. 

Put simply, InnerSource operates just like open-source in that project teams invite, accept and reject PRs; provide quality documentation; and build them gradually. The main difference is that InnerSource is limited to a single organization—in our case, dm.

With InnerSource, we encourage you to make your Bitbucket repositories open to other internal teams so they can find out about your work, fix bugs, make PRs, and even add features that your own team currently has no time to develop. 

**Where InnerSource projects belong**: Bitbucket


## Project Basics

### Code Review

Ask your team and other peers to:
- review your code and check for information not to be made public
- install and
- test your project prior to public release. 

### Creating a README

#### Do:
- [Use this checklist](https://github.com/dm-drogeriemarkt/dm-howto-open-source/blob/master/READMEtemplate.md). 
- Break up text often, for better readability.
- Think about SEO.

#### Don't:
- Refer to dm specifics, such as internal teams and processes
- Include large chunks of code without explaining what they represent
- Include any code that presents security vulnerabilities

#### Syntax and Formatting
Markdown is the simplest and most easily understood syntax; we recommend using it for all your documentation. However, we realize that there are exceptions. If Markdown isn’t practical, then we recommend using only one [GitHub-supported](https://github.com/github/markup#markups) markup format.

### Official Namespace

The official namespace for our projects is ‘**de.dm**’, where applicable. The namespace ‘**de.filiadata**’ should be considered deprecated, and no longer used for new projects.

### Applying Changes

All repository changes, including those made by maintainers, should come from GitHub pull requests so that we can streamline review and change tracking (as per [GitHub Flow](https://guides.github.com/introduction/flow/)). Everyone should have their own fork, though you can still edit READMEs/documentation/related files with the GitHub “Edit” button. The ‘master’ branch should be the accepted development head; pull requests get merged there.

### Versioning

Version all project artifacts should be [semantically](http://semver.org/). Tag all versions in GitHub with the exact version name (like ‘0.1.0’; do not prefix tags with “v.” or similar). For a better user experience, use the GitHub “release notes” feature to add notes whenever you change something in the new version.

### Maintainers

Maintainers are the contact people for a project. They are also the only contributors who can package new versions and apply changes to the repository (i.e., merge pull requests). Every project must have at least one maintainer. 

The Open Source Guild reserves the right to contact maintainers to ensure a project remains active/maintained. If the project is not being maintained, we will work with you to either find a new maintainer or remove the project from our organization page. Please be responsive to all internal queries about your project and its status.

#### Can I Use My Private GitHub Account To Contribute?

Yes, you can. Feel free to create a GitHub account associated with your company email address, but that's not obligatory. If you want to use your private account, that's also fine.

#### Create a Maintainers File

Every project needs a ‘[MAINTAINERS](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/MAINTAINERS)’ file (listing all maintainers) at its root. Your build/packaging configuration file (e.g., [pom.xml for Maven](https://maven.apache.org/pom.html#Developers)) can fulfill the purpose of a MAINTAINERS file. Format:

     [full name] <email address>
     [second full name] <email address>
     etc.


#### Be Prompt and Responsive

Respond promptly to pull requests and issues. “Within 72 hours” is a good window. Open issues do not make your project “look popular.” Instead, they make it look like you're neglecting your project. If project workload becomes unmanageable, ask the Guild or the community for help.

If you are away/on vacation and can’t respond to PRs/issues promptly, find someone who can.

If you're not going to accept a PR, reject it ASAP and include a brief explanation why.

If you're feeling maintainer burnout or facing some trolling behavior, give Jon Schinklert's [Maintainers Guide to Staying Positive](https://github.com/jonschlinkert/maintainers-guide-to-staying-positive) a read; it might help you to feel better.

#### Use Issues Creatively

Issues can be good for planning or for onboarding contributors. Issues should include a description of the point, question, discovery, or other detail prompting the issue.

Issues that consist solely of a title appear unprofessional and do not do much to invite discussion from the community.

Label your issues with clear tags. This is a great way to organize and categorize issues.



### Stay Secure

##### Two-Factor Authentication Is Required
GitHub organization members must enable [Two-Factor Authentication (2FA/MFA)](https://help.github.com/articles/about-two-factor-authentication/) in keeping with our Open Source First principle to "Stay Secure." Read [GitHub's post on 2FA](https://help.github.com/articles/about-two-factor-authentication/) for more information.

Don't have a smartphone, and/or want to give your phone number to GitHub? According to GitHub support, SMS or a TOTP app are currently the only primary 2FA methods that work. There are mobile and desktop TOTP apps that also work. See [GitHub's article on 2FA via TOTP apps](https://help.github.com/articles/configuring-two-factor-authentication-via-a-totp-mobile-app/) for more information. You can set up 2FA with a Google Voice SMS number, but should add a U2F device as backup.



### About Licensing

#### Quick FAQ

##### Which license do we use?
[The MIT license](https://opensource.org/licenses/MIT). MIT is succinct, straightforward, and easy use in closed-source projects. It allows the most broad usage of our source code, and keeps open-sourcing easy and safe. You must include a separate license file in your repository with the entire text of the MIT license included. 

If your project uses the MIT license and incorporates third-party OSS components, then you must attach this sentence in your license file: “This software is licensed under the MIT license (see below), unless otherwise stated in the license files in higher directories (if any)." Please also provide the license files for every third-party source you add.

[This helpful blog post](https://writing.kemitchell.com/2016/09/21/MIT-License-Line-by-Line.html) breaks down the license line by line for you. (If you're really interested in open source licensing, check out [Rosenlaw & Einschlag's free online book](http://www.rosenlaw.com/oslbook.htm) and/or [O'Reilly's/Andrew M. St. Laurent's](http://www.oreilly.com/openbook/osfreesoft/book/). These are a little dated, but still useful.)

For documents like this how-to, we recommend using [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/).

##### Must I use MIT?
Yes, for all newly created open-source projects.

##### I don't like the MIT license. Can I use another license?
Not without a compelling reason.

##### What if I fork an external project and/or contribute to it?
Keep the original license.

##### What if my team uses an external project whose license is not dm-recommended?
You can can use GPL code — but only internally. Be sure it's a version of the GPL that continues to allow for the ASP loophole. AGPL and versions of the GPL with additional restrictions won't work.

##### Who is the license owner?
dm-drogerie markt GmbH & Co. KG

##### Does my project need a LICENSE file?
Yes, at the root of the repository that contains the copy of the selected license (see above). [Here is an example](https://opensource.org/licenses/MIT) for MIT.

##### Do I need to add a license header to every source file?
No. In fact, we discourage it because it blows up file sizes, requires some build checking/pre-processing, and sometimes leads to situations [like this](http://trillian.mit.edu/~jc/humor/ATT_Copyright_true.html). It's also not needed for the licenses we use. Having one `LICENSE` file in the repository is enough.

##### What about a README note?

Yep. Every README{.md,.rst} file must state the following at the end:

>The MIT License (MIT)
>Copyright © [yyyy] dm-drogerie markt GmbH & Co. KG, https://dm.de

>Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the “Software”), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

>The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

>THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
>

Replace the [yyyy] field with the year that you created the project, and do not update it. Do not provide multiple years.

##### I still have licensing questions. What can I do?

Ask the Open Source Guild or Architecture Guild. See also our internal Open Source wiki page for detailed information and contact to legal help.

#### Repository of Meta Information

Many package managers include a feature to make the applied license machine readable. Use these! An example for [Maven](https://maven.apache.org/pom.html#Licenses):

```xml
<licenses>
    <license>
        <name>MIT</name>
        <url>https://opensource.org/licenses/MIT</url>
        <distribution>repo</distribution>
    </license>
</licenses>
```

An example for [Node](https://docs.npmjs.com/files/package.json#license), according to [this](https://gist.github.com/robertkowalski/7620849):

```
“license”: “MIT”
```

#### Restrictions Imposed by the License
“Dependency” typically means “being linked with,” “included in your artifact,” or “depends on it during runtime.” Dependencies can limit you. To remain in compliance, check the licenses of your projects. Your build tool’s license does not affect your software’s license. A jar file dependency will affect your software.


### Other Repository Information

#### JVM Artifacts
Host JVM artifacts (*.jar) on Maven Central in [the ‘de.dm’ group](https://repo1.maven.org/maven2/de/dm/). To do this, get a [Sonatype](http://central.sonatype.org/) account. If you don't have an account yet, register with Sonatype using your dm email address.

If you want to push to Sonatype but not to *.dm, register a different Sonatype account with a non-dm email address.

<!---
#### Node Modules
[Node](https://www.npmjs.com/) modules [now have namespaces](http://blog.npmjs.org/post/116936804365/solving-npms-hard-problem-naming-packages). Prefix them with a short product name: e.g. [karma](https://karma-runner.github.io/0.12/index.html) plugins are prefixed “karma-”; the same goes for gulp, grunt, etc. Host your Node modules in the public NPM registry. Here is [how to publish to NPM](https://gist.github.com/coolaj86/1318304).

#### Docker Images
You can currently browse it [here](https://registry.opensource.zalan.do/ui/), or with the Pier One command line utility. We have an [open source registry](https://registry.opensource.zalan.do/ui/) that everyone can read. It is deployed in the AWS open source account and Docker images can be pushed by any team member to their respective team repo:

```bash
$ # you need to login to registry-write.opensource.zalan.do (workaround for Docker V2 bug)
$ pierone login --url registry-write.opensource.zalan.do
$ docker push registry-write.opensource.zalan.do/myteam/myartifact:1.0
$ # on any other computer:
$ docker pull registry.opensource.zalan.do/myteam/myartifact:1.0 # no auth needed for download!
```
--->


### Working with External Contributors

We enthusiastically support you in recruiting non-dm contributors to work on your project. Collaboration and community are part of the fun of open source. 

Give GitHub's ["Creating a new contributor on-ramp" doc](https://github.com/blog/2128-creating-a-new-contributor-on-ramp) a look for some expert guidance. (TL;DR version = be welcoming, inclusive, and clear about what sorts of contributions you're looking for most).

Please ask external contributors to sign a contributor licensing agreement (CLA). Some thoughts on the importance of CLA in "professional open source" by [jooq](https://blog.jooq.org/2014/03/31/open-source-completely-underestimates-contributor-license-agreements/). A few good models to follow and adapt: [.Net Foundation](https://cla2.dotnetfoundation.org/) example (electronic submission via GitHub account); [Google’s CLA](https://github.com/angular/angular.js/blob/master/CONTRIBUTING.md#-signing-the-cla) for contributing to AngularJS is a simple click-through form with a Googlebot that automatically checks for signatures; Selenium/Software Freedom Conservancy uses a [Google form](https://docs.google.com/a/zalando.de/forms/d/11Z8LoYpTGUIwCegifVH1YtL9smxVDNk-fOykUZTAWhE/viewform?hl=en_US&formkey=dFFjXzBzM1VwekFlOWFWMjFFRjJMRFE6MQ#gid=0).



### Project Promotion

#### Proactively Communicate

Share your project with:
- relevant Xing/Linkedin groups
- community forums/boards
- e-newsletters and websites/newsletters dedicated to the problem(s) your project is trying to solve, the relevant languages, etc.
- if you have contacts at a university, pitch your project to their students
- major players in the industry


### Contributing to Non-dm Open-Source Projects

We encourage you to contribute to other open-source projects in ways that benefit dm. Some ways you might contribute:

- making bug fixes to libs you're using on the job
- pitching a feature request that your team/dept needs to a project we're using, getting confirmation from the maintainers to go forward, and doing the work
  - a good idea is to review the project's GitHub Issues Tracker to see if anyone else has made the same feature request; restart that conversation and see if you can get them + others to work collaboratively to make the needed change 

<!---
##### CLAs 

For typical CLAs, we are safe — but ask our legal team (guild can provide their contact info) to double-check whenever you’re in doubt. CLAs that are safe: Oracle, Apache, Google Projects.
--->
