# CFEngine Health Check

**Purpose**: Provide CFEngineers with a compact checklist for assessing CFEngine health.

**Bibliography**
This document is based on the following best-practice guides:
- [CFEngine 3 Best Practices (Archive)][1]
- [CFEngine Enterprise Best Practices][2]
- [Evolve Thinking's Best Practices][3]
 
[1]: https://auth.cfengine.com/archive/manuals/cf3-bestpractice                   
[2]: https://docs.cfengine.com/latest/enterprise-cfengine-guide-best-practices.html   
[3]: http://evolvethinking.com/category/cfengine/best-practices/    

**Contributors**: 
- Aleksey Tsalolikhin
- Nick Anderson
- Neil Watson
- Joe Moore

## Writing Policy

### Thinking CFEngine
- Do not think procedurally, instead declare your intentions as CFEngine promises. http://evolvethinking.com/cfengine-best-practices-part-2/
- Less is more, leave decisions on how to do something to CFEngine. http://evolvethinking.com/cfengine-best-practices-part-2/
- Focus on the end goal, not the procedure. http://evolvethinking.com/cfengine-best-practices-part-2/
- Don't try to control the order of execution. [Always keep coding to a minimum.](https://auth.cfengine.com/manuals/cf3-bestpractice#Always-keep-coding-to-a-minimum) [Embrace normal ordering.](http://evolvethinking.com/cfengine-best-practices-part-2/)

### Style
- Follow a consistent [policy style](https://docs.cfengine.com/latest/guide-writing-and-serving-policy-policy-style.html).
- Keep your policy in bundles and files to manageable amounts, making it easier to understand. Don't group together things that should be separate. [Arranging files.](https://auth.cfengine.com/archive/manuals/cf3-bestpractice#Arranging-files) [How to decide when to make a bundle.](https://auth.cfengine.com/archive/manuals/cf3-bestpractice#How-to-decide-when-to-make-a-bundle)
- Use meaningful names for your files and bundles. Make it obvious what they are about. [How to choose and name bundles.](https://auth.cfengine.com/archive/manuals/cf3-bestpractice#How-to-choose-and-name-bundles)
- Use naming conventions for bundles, handles, and classes. http://evolvethinking.com/cfengine-best-practices-part-2/

### Make and Use Libraries
- Don't duplicate code when you could use parameterized bundles. [When to use a parameterized bundle or method.](https://auth.cfengine.com/archive/manuals/cf3-bestpractice#When-to-use-a-paramaterized-bundle-or-method) [Build reusable bundles.](http://evolvethinking.com/cfengine-best-practices-part-2/)
- Don't reinvent the wheel. [CFEngine Standard Library](https://auth.cfengine.com/manuals/cf3-bestpractice#Always-use-existing-templates) [Use frameworks](http://evolvethinking.com/cfengine-best-practices-part-2/)
- Keep a site library instead of modifying CFEngine Standard Library.


### Document
- Always document the intention of your promises using ["comment"](https://auth.cfengine.com/archive/manuals/cf3-bestpractice#Always-document-promises) attribute.
- Use "promisees" to document who or what will be impacted by your promises.
- Use "meta" promises and attributes to document metadata such as who wrote the code, when, etc. (e.g. meta => { "author=John Smith", "version="2.0" }; ) 



### Classes Promises
- Classify your system before making changes to it. (Put class bundles first in bundlesequence.)
- Put classes in common bundles when you need to use them in multiple bundles. [When should classes be in common bundles?](https://auth.cfengine.com/archive/manuals/cf3-bestpractice#When-should-classes-be-in-common-bundles)


### Variables Promises
- Define your variables in the current bundle or in a common generic global bundle as much as possible. [When should variables be in common bundles?](https://auth.cfengine.com/manuals/cf3-bestpractice#When-should-variables-be-in-common-bundles) [When should variables be in local bundles?](https://auth.cfengine.com/archive/manuals/cf3-bestpractice#When-should-variables-be-in-local-bundles)
- [Use variables as pointers to paths and servers, rather than coding them directly into promises.](https://auth.cfengine.com/manuals/cf3-bestpractice#Always-use-variables-as-pointers-to-paths-and-servers)
- [Always use lists to make the same promise about multiple objects.](https://auth.cfengine.com/manuals/cf3-bestpractice#Always-use-lists-to-make-the-same-promise-about-multiple-objects)

### Commands Promises
- Don't embed shell commands in policy when you could use native CFEngine code.  [Never embed simple shell commands.](https://auth.cfengine.com/archive/manuals/cf3-bestpractice#Never-embed-simple-shell-commands) [Avoid writing custom scripts](https://auth.cfengine.com/manuals/cf3-bestpractice#Avoid-writing-custom-scripts) [Use shell commands sparingly.](http://evolvethinking.com/cfengine-best-practices-part-2/) [Beware the shell environment.](http://evolvethinking.com/cfengine-best-practices-part-2/) [Don't use command promises to cheat.](http://evolvethinking.com/cfengine-best-practices-part-2/) 
- [Always use system variables to get information about system resources, rather than running external commands.](https://auth.cfengine.com/manuals/cf3-bestpractice#Always-use-the-system-variables-for-system-resources)

### Files Promises
- Use separate promises for file permissions and content. http://evolvethinking.com/cfengine-best-practices-part-2/
- Avoid promises that are too broad. http://evolvethinking.com/cfengine-best-practices-part-2/
- Promise whole files and not just a portion of a file. http://evolvethinking.com/cfengine-best-practices-part-2/
- [Try to combine tests and operations during file searches](https://auth.cfengine.com/archive/manuals/cf3-bestpractice#Try-to-combine-tests-and-operations-during-file-searches)

### Collaborating with others
- Use [branch and merge](http://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging) workflows.
- [Delegate responsibility](https://auth.cfengine.com/manuals/cf3-bestpractice#Delegating-responsibility) if appropriate in your organization. Vet and agglomerate policy from different sources.

### Handling secrets
- Don't put secrets in your policy. Use cf-keycrypt, a password vault or GPG to secure your secrets. http://cfengine.com/wp-content/uploads/2015/02/cfgcamp-2015.pdf
- If you put secrets in your policy, you can limit selected inputs to agents, but do so with caution. http://evolvethinking.com/cfengine-best-practices-deployment-upgrades-and-scaling/

### Misc.
- Use version control, everywhere. http://evolvethinking.com/cfengine-best-practices-deployment-upgrades-and-scaling/
- Start with [simple prototypes](http://evolvethinking.com/cfengine-best-practices-testing/).
- Don't maintain cron jobs - use CFEngine's time classes. [Never manage more than one cron job](https://auth.cfengine.com/archive/manuals/cf3-bestpractice#Never-manage-more-than-one-cron-job)
- Separate data from policy. http://evolvethinking.com/cfengine-best-practices-part-2/
- Make policy reliable even when the server is unavailable. http://evolvethinking.com/cfengine-best-practices-deployment-upgrades-and-scaling/
- Don't mess with update.cf or failsafe.cf http://evolvethinking.com/cfengine-best-practices-part-2/
- [Label new policy items uniquely for tracking.](https://auth.cfengine.com/archive/manuals/cf3-bestpractice#Policy-changes)


## Quality Control / Testing 

- Use editor plugins to provide syntax highlighting to catch errors early.
- Use a pre-commit hook to catch errors early. Or use automated testing of policy (Jenkins, etc.) before distributing it. [Check syntax with cf-promises](http://evolvethinking.com/cfengine-best-practices-testing/)
- Try to [test formally](http://evolvethinking.com/cfengine-best-practices-testing/), including unit tests.
- Test on multiple architectures. Use reporting for [scale](http://evolvethinking.com/cfengine-best-practices-testing/).



## Making Changes to Production

- [Never change system policy when humans are absent](https://auth.cfengine.com/archive/manuals/cf3-bestpractice#Never-change-system-policy-when-humans-are-absent)
- [Try to make many small changes rather than one large change to reduce risk.](https://auth.cfengine.com/archive/manuals/cf3-bestpractice#Try-to-make-many-small-changes)
- [Think through your changes](https://auth.cfengine.com/archive/manuals/cf3-bestpractice#Policy-changes)
- [Have a policy and schedule concerning major changes.](https://auth.cfengine.com/archive/manuals/cf3-bestpractice#Policy-changes)
- [Test prior to releasing to production environment.](https://auth.cfengine.com/archive/manuals/cf3-bestpractice#Policy-changes)
- [Test in the production environment on a small number of machines whenever possible.](https://auth.cfengine.com/archive/manuals/cf3-bestpractice#Policy-changes)
- Develop a process for deploying changes in progressive waves to decrease risk.
- Consider a ["default_repository"](https://auth.cfengine.com/archive/manuals/cf3-bestpractice#Configuration-version-control-and-rollback) in case you have to examine history of changes to files managed by CFEngine.


## Hub health
- Run your CFEngine Postgres database on a [dedicated SSD](https://docs.cfengine.com/latest/enterprise-cfengine-guide-best-practices.html#scalability) for best performance.
- Set ["splaytime"](https://docs.cfengine.com/latest/enterprise-cfengine-guide-best-practices.html#scalability) to reduce load on your hub.
- Monitor Hub server utilization to make sure it's within normal parameters with room to spare.
- Have more than one hub in case your hub dies or has hardware issues, of the same grade of hardware so it can handle full production load.
- Clean up your hub to remove entries for nodes that have been decommissioned (to improve hub performance and increase readability for humans).
- Use splaytime and ifelasped to reduce agent and server load. http://evolvethinking.com/cfengine-best-practices-deployment-upgrades-and-scaling/
- Make CFEngine policy servers in redundant pairs. http://evolvethinking.com/cfengine-best-practices-deployment-upgrades-and-scaling/
- Try to stay up to date on your CFEngine software version as the software is continously improved.


### Upgrades
- CFEngine 2 and 3 can run in parallel for gradual migration. http://evolvethinking.com/cfengine-best-practices-deployment-upgrades-and-scaling/
- Upgrade policy and CFEngine 3 with extensive planning and testing. http://evolvethinking.com/cfengine-best-practices-deployment-upgrades-and-scaling/



## Using CFEngine
- [Use cf-monitord to detect and investigate anomalies to understand and increase system stability.](https://auth.cfengine.com/manuals/cf3-bestpractice#Anomaly-Monitoring)
- [Don't run housekeeping tasks (such as updating databases or performing business tasks) every time CFEngine runs. Use "ifelapsed".](https://auth.cfengine.com/manuals/cf3-bestpractice#Batch-Jobs)
- [Collect garbage on your systems (e.g. remove old log files)](https://auth.cfengine.com/manuals/cf3-bestpractice#Garbage-Collection)
- [Manage name service (/etc/resolv.conf)](https://auth.cfengine.com/manuals/cf3-bestpractice#Name-Service)
- [Have a policy definition point for your system, to facilitate distributing policy updates.](https://auth.cfengine.com/manuals/cf3-bestpractice#Policy-Distribution)
- [Use CFEngine to ensure your services stay up and running, or to take down services that should not be running.](https://auth.cfengine.com/manuals/cf3-bestpractice#Services)
- [Have a site security policy. Use CFEngine to implement hardening measures, and to monitor important assets.](https://auth.cfengine.com/manuals/cf3-bestpractice#Security)
- [Use packages (rather than tarballs or building from source) to install software.](https://auth.cfengine.com/manuals/cf3-bestpractice#Software-Management)
- [Avoid running CFEngine without lock protection](https://auth.cfengine.com/archive/manuals/cf3-bestpractice#Avoid-running-CFEngine-without-lock-protection)
- Always monitor promise compliance and investigate non-compliances.
- Don't install CFEngine RPM onto an image and then "bake" and deploy the image, as your nodes will have the same key which will cause management headaches and performance issues. Install CFEngine during node initialization.
- Setup your policy hub to update "masterfiles" from Version Control to [automate policy distribution](https://docs.cfengine.com/latest/enterprise-cfengine-guide-best-practices.html#version-control-and-configuration-policy).


## TODO
When this document settles down, open a pull request to
https://github.com/cfengine/documentation/ in
https://github.com/cfengine/documentation/tree/master/guide/writing-and-serving-policy
