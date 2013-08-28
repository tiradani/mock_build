mock_build
==========

Wrapper script for building RPMs directly from a git repository using mock.


There are some assumptions built into this script.  The environment I work in requires kerberos 
authentication for ssh access.  Additionally, exemptions are required to enable http(s) access to 
servers.  Since http(s) access is a non-starter and Mock doesn't play nice with kerberos 
(especially on Fedora 18+), we assume that you locally clone the repository, then provide the 
full path to the clone to the script.

A few other assumptions:

* mock-scm has been installed
* The spec file is named the same as your repository name
* mock-scm builds a source tarball for you, but includes the base directory in the tarball.

    Therefore, in your %install section, when you want to refer to a file in the tarball, you must include the base directory as well.  

    example:

    Instead of:

    ```cp -r etc/your_project/some_config_file $RPM_BUILD_ROOT%{_sysconfdir}/your_project```

    You must now have:

    ```cp -r your_project-%{version}/etc/your_project/some_config_file $RPM_BUILD_ROOT%{_sysconfdir}/your_project```

