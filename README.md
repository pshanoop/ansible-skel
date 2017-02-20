# ansible-skel
This is my Ansible skeleton. It provide a nice structure to work comfortably with Ansible. You don't need to follow all principes of this structure to use Ansible.


## Goal and features

The goal of this template is to provide a quick way to start with Ansible. It is a mix of best practices gathered around the web and the result of my own experience. You will find here an extremely modular structure, which should not let the user doubt where to put the correct files. Some advanced topics are covered into [the docs folder](docs/)

Basically, this structure provides:

- A nice default ```ansible.cfg``` file
- A way to organise hosts and groups
- An efficient way to organise variables, depending hosts, groups or environments
- It helps to avoid the recommended messy structure
- Most of files are grouped under directories to avoid confusion
- Provide a nice subset of plugins
- Provide default playbooks to really start quickly your development
- Most of file are shortly documented, with a description of most common patterns

So, just clone this repo, and start to dev :-)


## Quick Start

To help you to start quickly, there are few entrey point to have your first playbook working. First, you need to add the targets you want to manage:

```
vim inventory/default.ini
```
Then add your target hosts under the ```[targets]``` section. If you feel lost, checkout the examples inside the file. Once you have done that, you can run the first playbook, which will ensure you have all required roles. If you don't have them, it will download them from [Ansible Galaxy](https://galaxy.ansible.com/) or from a git repo depending the source. It will install them into ```roles/vendors```.

```
ansible-playbook playbooks/0_local_requirements.yaml
```
Once you get there, you are sure you have all requirements to play with Ansible. Then, we will ensure your inventory is correct by trying to connect on all hosts. Obviously, this playbook will not modify at this stage your targets, it's just to be sure your inventory is ok.
```
ansible-playbook playbooks/1_target_test.yml
```
If it run without errors, you can start to develop you own playbooks and roles. Enjoy!


## File structure
The files structure is organised this way:
```
.
├── LICENSE
├── README.md                             # Documentation entry point
├── ansible.cfg -> config/ansible.cfg     # Symlink to vagrant config
├── config                              # Configuration directory
│   ├── ansible.cfg                       # Ansible configuration
│   ├── ssh_config                        # SSH configuration
│   ├── tmp                               # Temporary files
│   └── vault_password                    # Default vault file
├── docs                                # Advanced documentation topics
│   ├── skel-start.md
│   └── skel-tips.md
├── group_vars                          # Group vars directory
│   ├── all.yml                           # Common variables to all hosts
│   ├── dev.yml                           # Dev env variables
│   ├── preprod.yml                       # Preprod env variables
│   └── prod.yml                          # Production env variables
├── host_vars                           # Host vars directory
├── inventory                           # Inventory directory
│   ├── default.ini -> dev.ini            # Default inventory to use
│   ├── dev.ini                           # Dev inventory
│   ├── preprod.ini                       # Preprod inventary
│   └── prod.ini                          # Production inventory
├── playbooks                           # Playbook directory
│   ├── 0_local_requirements.yaml         # Configure local system
│   ├── 1_target_test.yml                 # Test targets
│   ├── 2_target_requirements.yml         # Basic configuration of targets
│   └── 3_target_sysadmin.yml             # Advanced confivuration of targets
├── plugins                             # Plugin directory
│   ├── action                            # Action plugins
│   ├── callback                          # Callback plugins
│   ├── connection                        # Connection plugins
│   ├── filter                            # Filter plugins
│   ├── lookup                            # Lookup plugins
│   ├── modules                           # Modules plugins
│   └── vars                              # Vars plugins
└── roles                               # Roles directory
    ├── local                             # Locale roles
    ├── profiles                          # Profile roles
    ├── requirements.yml                  # Vendor roles list
    └── vendors                           # Vendor roles
```

## Compatibility

This skeleton will mainly work with Ansible 2.2. It could run on lower versions, but it has not been tested. Definitely not compatible with 1.x branch. Please checkout the correct branch of this repo to get the matching version.

As this skeleton comes with some python plugins, you may need to install extra Python dependencies if you want to use them:

* string_utils: slugify
* ipaddr: netaddr

Usually, a simple ```pip install slugify netaddr``` should let use those plugins. At this stage, documentation for the plugins is pretty poor, and you may need to read the source code if you want to understand how to use them.

## Alternatives

Some other people has already made a such exercise, and there is below what I found. I would recommend you to try other esier skeletons if you are comfortable with Ansible:

* https://github.com/linsomniac/ansible-skeleton
* https://github.com/bertvv/ansible-skeleton
* https://github.com/mtpereira/ansible-skel
* https://github.com/mattjbarlow/ansible-directory


## Contributing

The git log is historically a bit messy. To avoid this pattern, and help colaborators to work on it, we assume the following convention:

* **Feat**: A new feature
* **Fix**: A bug fix
* **Change**: A behaviour
* **Docs**: Documentation only changes
* **Style**: Changes that do not affect the meaning of the code (white-space, formatting, missing
  seMi-colons, etc)
* **Refactor**: A code change that neither fixes a bug nor adds a feature
* **Clean**: A portion of legacy code
* **Perf**: A code change that improves performance
* **Test**: Adding missing or correcting existing tests
* **Chore**: Changes to the build process or auxiliary tools and libraries such as documentation
  generation


Each commit message must have a maximum lenght of 72 characters. The title must follow the imperative at the present tense. The title must start with an uppercase letter, and there is no dot at the end of the sentence. An easy way to remember is: ''if applied, this commit will <commit_title>''. Optionnaly, it is a good practice to add some explanations of what the commit do.

Examples:

* Feat: Create an internal role to test target connection
* Clean: Remove legacy commented code in helpers
* Docs: Update the documentation about commit messages convention

## Releases

* 0.5 - 26/01/2017
  * Compatibility  for Ansible-2.2 
  * Make some clean, stabilise the code
  * Update the documentation documentation

## License

Please read [GNU GENERAL PUBLIC LICENSE](LICENSE).

## Credits
There are a lot of goood ideas taken from the [enginyoyen ansible best practice repository](https://github.com/enginyoyen/ansible-best-practises/). The rest comes from some colleagues (Hi [Simon](https://github.com/spiette) !) and my customer experience.


Ansible-skel by skel:
``` text
           .-. 
 {`:      (o.O)
  \\       |~| 
   \\     __|__
     o===o.=|=.o\
          .=|=. \\
          .=|=. ::}  
           _=_  
          ( _ )   
          || ||
          || ||
          () ()
          || ||
          || ||
         ==' '== 
```
Inspired from l42 work.

