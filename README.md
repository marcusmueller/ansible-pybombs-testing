# Automated pybombs testing

This allows you to quickly get pybombs to build GNU Radio on a set of freshly provisioned VMs.

## Usage

### Requirements

Host
----

* ansible in a somewhat recent version (I tested with 1.9.something)
* if you haven't done `git clone --recursive`, this is probably a good time to `git submodule init`

Targets
-------

* `~root/.ssh/authorized_keys` containing your public key (i.e. you need to be able to log in as root without being prompted a password)


### Setting up

Hosts
-----

Edit the `default.inventory` file to contain your hosts of choice. I used aliases to make my logs easier to read.

Run

    $ ansible -i default.inventory gnuradio-vms -m ping

to verify all machines are reachable and willing to *cooperate* (read this in a Dalek voice for maximum satisfaction).

Configuring the playbook
------------------------

Next, modify `pybombs.yml`; you should replace the `staging_repo` and `staging_branch` variables at the top with what you want to try; if you just want stay with the mainline `gr-recipes`, just use 

          vars:
                  staging_repo: origin
                  staging_branch: master
                  pybombs_pip: pybombs

Running
-------

     $ ansible-playbook  -i default.inventory pybombs.yml
