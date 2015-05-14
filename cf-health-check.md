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

## Section I
Based on [CFEngine 3 Best Practices][1].

### Policy Style
- Follow a consistent [policy style](https://docs.cfengine.com/latest/guide-writing-and-serving-policy-policy-style.html).
- Keep your policy in bundles and files to manageable amounts, making it easier to understand. Don't group together things that should be separate. [Arranging files.](https://auth.cfengine.com/archive/manuals/cf3-bestpractice#Arranging-files) [How to decide when to make a bundle.](https://auth.cfengine.com/archive/manuals/cf3-bestpractice#How-to-decide-when-to-make-a-bundle)
- Use meaningful names for your files and bundles. Make it obvious what they are about. [How to choose and name bundles.](https://auth.cfengine.com/archive/manuals/cf3-bestpractice#How-to-choose-and-name-bundles)
- Define your variables in current bundle or in a common generic global bundle as much as possible. [When should variables be in common bundles?](https://auth.cfengine.com/manuals/cf3-bestpractice#When-should-variables-be-in-common-bundles) [When should variables be in local bundles?](https://auth.cfengine.com/archive/manuals/cf3-bestpractice#When-should-variables-be-in-local-bundles)
- Put classes in common bundles when you need to use them in multiple bundles. [When should classes be in common bundles?](https://auth.cfengine.com/archive/manuals/cf3-bestpractice#When-should-classes-be-in-common-bundles)
- Don't duplicate code when you could use parameterized bundles. [When to use a parameterized bundle or method.](https://auth.cfengine.com/archive/manuals/cf3-bestpractice#When-to-use-a-paramaterized-bundle-or-method)
- Classify your system before making changes to it.

### Do’s and Don’ts
- Don't make policy changes made when humans aren’t around (e.g. just before going offline for the weekend).
- Don't embed shell commands in policy when you could use native CFEngine code.
- Don't maintain cron jobs - use CFEngine's time classes.
- Don't run CFEngine without lock protection (cf-agent -K).
- When doing file searches, combine operations to reduce load.
- Make many small changes rather than one large change to reduce risk.
- Use "comment" attributes to explain the intention of your promises.
- Use "promisees" to document who or what will be impacted by your promises.
- Use "meta" promises and attributes to document metadata such as who wrote the code, etc.. (e.g. meta => { "author=John Smith", "version="2.0" }; ) 
- Don't try to control the order of execution in your policy. Don't fight Normal Ordering.
- Use lists to make the same promise about multiple objects, rather than coding the same promise many times.
- Use the CFEngine Standard Library rather than re-inventing the wheel.
- Use CFEngine policy frameworks (NCF or EFL) to add functionality and make it easier and safer for your system administrators to create new policies.
- Use system variables to get information about system resources, rather than running external commands.
- Use variables as pointers to paths and servers, rather than coding them directly into promises.

### Workflows
- Use cf-monitord to detect and investigate anomalies to understand and increase system stability.
- Don’t run housekeeping tasks (such as updating databases or performing business tasks) every time CFEngine runs. Use "ifelapsed".
- Collect garbage on your systems (e.g. remove old log files)
- Manage name service (/etc/resolv.conf)
- Have a policy definition point for your system, to facilitate distributing policy updates.
- Use CFEngine to ensure your services stay up and running, or to take down services that should not be running.
- Have a site security policy. Use CFEngine to implement hardening measures, and to monitor important assets.
- Use packages (rather than tarballs or building from source) to install software.

### Quality Assurance
- Have a policy and schedule concerning major changes.
- Label new policy items uniquely for tracking.
- Test prior to releasing to production environment.
- Test in the production environment on a small number of machines whenever possible.
- Develop a process for deploying changes as progressive waves to decrease risk.
- Define a "default_repository" in case you have to examine history of changes to files managed by CFEngine.
- Delegate responsibility if appropriate in your organization. Vet and agglomerate policy from different sources.

## Section II
Based on [CFEngine Enterprise Best Practices][2].

- Keep your source code in version control.
- Use [branch and merge workflows](http://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging).
- Setup your hub to update "masterfiles" from Version Control to automate policy distribution.
- Run your CFEngine Postgres database on a dedicated SSD for best performance.
- Set "splaytime" to reduce load on your hub.

## Section III
Based on our experience.

- Monitor Hub server utilization to make sure it's within normal parameters with room to spare.
- Have more than one hub in case your hub dies or has hardware issues, of the same grade of hardware so it can handle full production load.
- Clean up your hub to remove entries for nodes that have been decommissioned (to improve hub performance and increase readability for humans).
- Monitor promise compliance and investigate non-compliances.
- Don't install CFEngine RPM onto an image and then "bake" and re-use that image, as your nodes will have the same key which will cause management headaches and performance issues.
- Use a syntax highlighter when editing to catch errors early.
- Use a pre-commit hook to catch errors. Or use automated testing of policy (Jenkins, etc.) before distributing it.
- Learn CFEngine (from "Learning CFEngine 3" book, online documentation and trainings, and professional training, etc.).
- Don't put secrets in your policy. Use cf-keycrypt, a password vault or GPG to secure your secrets.

## Section IV
[Evolve Thinking's Best Practices][3]

````
### Testing Best Practices

Start with simple prototypes.
Use editor plugins.
Check syntax with cf-promises.
Test formally, including unit tests.
Test on multiple architectures. Use reporting for scale.


### More
Do not think procedurally, instead declare your intentions as CFEngine promises.
Less is more, leave decisions on how to do something to CFEngine.
Focus on the end goal, not the procedure.
Build reusable bundles.
Separation data form policy.
Promise whole files and not just a portion of a file.
Make your policy readable.
Use naming conventions for bundles, handles, and classes.
Use separate promises for file permissions and content.
Embrace normal ordering.
Use shell commands sparingly.
Beware the shell environment.
Don’t use command promises to cheat.
Avoid promises that are too broad.
Don’t mess with update.cf or failsafe.cf

### And more
Use version control, everywhere.
CFEngine 2 and 3 can run in parallel for gradual migration.
Upgrade policy and CFEngine 3 with extensive planning and testing.
Use splaytime and ifelasped to reduce agent and server load.
Make CFEngine policy servers in redundant pairs.
Make policy reliable even when the server is unavailable.
You can limit selected inputs to agents, but do so with caution.

````

## TODO
When this document settles down, open a pull request to
https://github.com/cfengine/documentation/ in
https://github.com/cfengine/documentation/tree/master/guide/writing-and-serving-policy
