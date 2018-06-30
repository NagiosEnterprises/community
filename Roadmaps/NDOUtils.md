# NDOUtils Roadmap

## Repository Consistency

We're on a mission to ensure that the open source projects are consistent
with each other. This check list will be here until that objective has
been completed. An identical check list exists in the other open source
roadmaps as well.

 - [ ] All text documents converted to Mark Down documents
 - [ ] README links to the Community repository
     - [ ] README contains a reference to the Code of Conduct
     - [ ] README contains a reference to the Contributing guide
     - [ ] README contains a reference to the Coding Styles
     - [ ] README contains a reference to the appropriate Roadmap
 - [ ] Changelog converted to Mark Down, and named CHANGELOG.md
 - [ ] Has consistent top level documents
     - [x] README.md
     - [ ] INSTALLING.md
     - [ ] UPGRADING.md
     - [ ] THANKS.md
     - [ ] LICENSE
     - [ ] LEGAL.md
 - [ ] Project uses Travis CI tests
     - [ ] Travis CI output contains a coverage report
     - [ ] Tests considered to be generally useful
 - [ ] Next maintenance, enhancement, and major release milestones created
 - [ ] All open issues assigned an appropriate milestone
 - [ ] Issue template created
 - [ ] Move any `*.m4` files into the `configure.ac`
 - [ ] Migrate `autoconf-macros` and/or any `*.m4` files into a `macros/` directory
 - [ ] All configuration files to be used moved to `config/` directory
 - [x] All startup/daemon/init related scripts and binaries moved to `startup/` directory
 - [ ] All scripts/executables used for repository management (e.g.: `update-version.sh`)
       moved to a `tools/` directory
 - [ ] All automated testing contained in a `test/` directory
 - [ ] All source code contained in a `src/` directory
 - [ ] All header files contained in an `include/` directory (even library headers)
 - [ ] All package related files contained in a `pkg/` directory
