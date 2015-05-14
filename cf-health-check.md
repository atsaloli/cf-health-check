# CFEngine Health Check

**Purpose**: Provide CFEngineers with a compact checklist for assessing CFEngine health.

**Bibliography**: 
This document is based on the following best-practice  guides - read them first:
- [CFEngine 3 Best Practices (Archive)][1]
- [CFEngine Enterprise Best Practices][2]
- [Evolve Thinking's Best Practices][3]
 
[1]: https://auth.cfengine.com/archive/manuals/cf3-bestpractice                   
[2]: https://docs.cfengine.com/latest/enterprise-cfengine-guide-best-practices.html   
[3]: http://evolvethinking.com/category/cfengine/best-practices/    

**Contributors**: Aleksey Tsalolikhin, Nick Anderson, Neil Watson

Feedback and contributions welcome!

----------------------------

## Section I
Section I is based on [CFEngine 3 Best Practices][1].

### Policy Style
- (Do) Do you follow a consistent policy style?
See [Policy Style Guide](https://docs.cfengine.com/latest/guide-writing-and-serving-policy-policy-style.html)
-	(Do) Is the policy broken down into separate files, keeping the scope of the policy to manageable amounts, making it easier to understand?
-	(Do) Are variables defined as close to the place where they are used as possible? (in the current bundle, first and foremost; or in some common bundle for generic, global data.  As opposed to in some other agent bundle -- unless you are passing the variable name as a parameter.) 
-	(Do) Are bundle names meaningful?  Does the name make clear to a non-expert what the bundle is about?
-	(Don’t) Are things bundled together that don’t belong together?  (Are bundles too big?)
-	(Don’t) Is code duplicated instead of using parameterized bundles?
-	(Do) Do you put classes in common bundles when you need to use them in multiple bundles?
-	(Do) Do you classify your system before starting to configure it?

### Do’s and Don’ts
-	(Don’t) Are policy changes made when humans aren’t around (e.g. just before going offline for the weekend?)
-	(Don’t) Are there shell commands embedded in policy instead of using native CFEngine code which is faster and convergent?
-	(Don’t) Does your policy maintain cron jobs instead of using CFEngine’s time classes?
-	(Don’t) Do you run CFEngine without lock protection? (cf-agent -K)
-	(Do) If you do file searches, do you combine operations to optimize resource use of the system?
-	(Do) Do you make many small changes rather than one large change to reduce risk?
-	(Do) Do you use "comment" attributes to explain the intention of your promises?
-	(Do) Do you use "promisees" to document who or what will be impacted by your promises?
-	(Do) Do you use "meta" promise attributes or "meta" promise type to document promise metadata such as who wrote the code? (e.g. meta => { "author=John Smith", "version="2.0" }; ) 
-	(Don’t) Do you try to control the order of execution in your policy?  (Do you try to get around Normal Ordering?)
-	(Do) Do you use lists to make the same promise about multiple objects, rather than coding the same promise many times?
-	(Do) Are you familiar with and do you use the CFEngine Standard Library rather than re-inventing the wheel?
-	(Do) Do you use system variables to get information about system resources, rather than running external commands?
-	(Do) Do you use variables as pointers to paths and servers, rather than coding them directly into promises?

### Workflows
-	(Do) Do you monitor for and investigate anomalies using cf-monitord to understand and increase system stability?
-	(Don’t) Do you run housekeeping tasks (such as updating databases or performing business tasks) jobs every time CFEngine runs? (Are you using "ifelapsed" to make sure you don't run external commands too often?)
-	(Do) Do you do garbage collection on your systems? (e.g. removing old log files)
-	(Do) Do you manage name service (/etc/resolv.conf)?
-	(Do) Do you have a policy definition point for your system, to facilitate distributing policy updates?
-	(Do) Do you use CFEngine to ensure your services stay up and running, or to take down services that should not be running?
-	(Do) Do you have a site security policy? Do you use CFEngine to implement hardening measures, and to monitor important assets?
-	(Do) Do you use packages (rather than tarballs or building from source) to install software?

### Quality Assurance
- (Do) Do you have a policy and schedule concerning major changes?
-	(Do) Are new policy items labeled uniquely for tracking?
-	(Do) Do you test prior to releasing to production environment?
-	(Do) Do you test in the production environment on a small number of machines whenever possible?
-	(Do) Do you maintain your policy set's revision number (preferably integrated with your VCS) in body common control using the “version” attribute to make it easily visible which hosts have old policies?
-	(Do) Do you have a “default_repository” defined in case you have to examine history of changes to files managed by CFEngine?
-	(Do) Do you delegate responsibility if appropriate in your organization? Do you vet and agglomerate policy from different sources?

## Section II
Section II is based on [CFEngine Enterprise Best Practices][2].

-	(Do) Is your source code in version control?  Are you using version control following modern best practices (e.g. [branch and merge workflows](http://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging))?  
-	(Do) Does your Hub integrate with a version control repository so that your "masterfiles" are automically updated to the latest version?  
-	(Do) Are you running your CFEngine Postgres database on dedicated SSD for best performance?
-	(Do) Do you set "splaytime" to reduce load on your hub?

## Section III
Section III is based on our experience.

-	(Do) Do you monitor Hub server utilization to make sure it's within normal parameters with room to spare?
-	(Do) Do you have more than one hub in case your hub dies or has hardware issues? Is it the same grade of hardware so you can be sure it can handle the full production load?
-	(Do) Do you clean up your hub to remove entries for nodes that have been decommissioned (to improve hub performance and increase readability for humans)?
-	(Do) Do you monitor promise compliance and investigate non-compliances?
-	(Do) Do your nodes have unique keys?  (Don't: If you installed the CFEngine RPM onto an image and then re-used that image, your nodes will have the same key which will cause management headaches and performance issues.)  
-	(Do) Do you use a syntax highlighter when editing code to catch errors early?
-	(Do) Do you use a pre-commit hook to catch errors? Or any automated testing of policy before it is available for remote agent distribution (such as Jenkins, etc.)
-	(Do) Have you studied “Learning CFEngine 3”?
-	(Do) Have you studied the CFEngine documentation?
-	(Do) Have you had professional training?
- (Don't) Do you put secrets in your policy?  (Passwords in plain text.) Or do you use cf-keycrypt or a password vault or GPG to secure your secrets?
- (Do) Do you have a process for deploying changes safely?  (Gradual, progressive rollout to ever-increasing numbers of servers to minimize risk)
- (Do) Do you use CFEngine policy frameworks (NCF or EFL) to add functionality and make it easier and safer for your system administrators to create new policies?

-----------------------
Neil Watson suggested:
 
Regarding the writing style. The question format makes a passive voice
style, and some of the questions are hard for newer users to understand.
Better to replace all the questions and be assertive telling the user
what they should do.
------------------------

Nick writes:

Feel free to open a pull request to
https://github.com/cfengine/documentation/

Probably
https://github.com/cfengine/documentation/tree/master/guide/writing-and-serving-policy
is a good place.
