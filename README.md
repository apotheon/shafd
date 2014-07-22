# Specification for Hierarchical Auxiliary File Defaults

This specification establishes a clear guide to the common practices of default
paths used to store auxiliary files for applications in the POSIX/Unix
developer culture.

## Specification

At present, the working copy of the specification is:

[Working Specification Document](doc/tip/spec.md)

## The State Of The World

POSIX/Unix applications often use configuration and data files that are
particular to those applications.  In cases where an application depends on
some other piece of software that defines its own defaults for file location,
as in the case of applications that make use of DBMSes such as PostgreSQL and
HTML servers like nginx, the application may offload the task of defining file
location defaults to that other software.  Where the application developer must
make his or her own decisions about where to place files by default within a
given application's design philosophy, however, the option to push the problem
off onto another application developer's choices is not available.

The ad-hoc approach has given rise to a few different takes on "best practice".
Three appear most notable: the FHS, the XDG Base Directory Specification, and
the emergent de facto standard approach of many of the rest of the POSIX/Unix
development world.

### FHS

The Filesystem Hierarchy Standard has emerged from the Linux community as an
attempt to homogenize practices for developers of Unix-like OSes and the
applications that run on them with regard to the organization of the virtual
filesystem.

While the FHS gives some guidance on where a developer may choose to place
files related to his or her application, that guidance is largely incidental
with regard to configuration and data files, and mostly silent with regard to
user-specific configuration and data files.  It is for this reason a group of
Linux developers chose to extend the FHS with the XDG Base Directory
Specification.

The FHS suffers some problems of its own, apart from its (lack of) direct
treatment of certain classes of application-specific files.  While some BSD
Unix developers were involved in the development of the FHS, as a process of
extending the older and more Linux-specific FSSTND (Filesystem Standard) to
apply to Unix-like systems in general, Linux development culture indelibly
marks the FHS with its departures from decades of common Unix practices and
tendency to encourage clutter in directories traditionally reserved for limited
use by the needs of the core system as well as arbitrarily deep subhierarchies
that can make navigation via shell or file browser inconvenient.

The design of the FHS, in an attempt to compromise between the practices of a
variety of different operating system projects, arrived at a standard that
tends to encourage proliferation of symlinks and hardlinks in default installs.
This becomes necessary because the FHS conflicts in some way with almost every
pre-existing operating system's virtual filesystem organizational principles.
To maintain backward compatibility with previous practices, OS developers
choose to either create links within the filesystem to satisfy the FHS or move
directories to comply and create links to provide backward compatibility,
resulting in unreasonable clutter.

While the goals of the FHS -- which involve making life easier for developers
by establishing a standard on which developers can rely when writing
cross-platform applications -- are noble, the execution has been one of
political compromise that, to some degree at least, fails to consider the
reasoning from experience that gave rise to many of the choices made in more
traditional filesystem hierarchies.

As a result of these issues, drawing specifically and primarily from the FHS
when choosing where to place application-specific files can tend to reinforce,
proliferate, and perpetuate the mistakes of the FHS.  While conforming to the
FHS as much as reasonably possible is a good idea for purposes of application
portability, "reasonable" requires doing so without ignoring the benefits of
conflicting filesystem hierarchy specifications.

### XDG BDS

Where the FHS deals with overall virtual filesystem design, it does not have
much to say about the choices made by applications with regard to their own
auxiliary file paths unrelated to the core system.  The XDG Base Directory
Specification is a freedesktop.org project that attempts to fill that gap.

A specification that explicitly establishes conformance to the FHS while
providing a clear and portable set of guidelines for defining the default paths
for the auxiliary files created and/or used by applications, including
user-level file path guidance, is in and of itself an excellent idea.  Even
better, the XDG BDS also does so in a way that provides for portable,
standardized approaches to defining non-default paths on an individual basis.

The XDG BDS itself, however, suffers some problems.  For example, it does not
take into account any filesystem hierarchy practices apart from the FHS in its
considerations, unless it takes them into account by consciously contradicting
them.  It makes decisions about how to organize things within FHS-compliant
virtual filesystem hierarchies that interpret the FHS in ways that may prove
counterproductive for both developers and users, such as by making the
necessities of auxiliary file tracking and default degradation overly complex
and difficult to find.  It also uses interpretations of the FHS in ways that
may tend to harm portability.

### De Facto POSIX/Unix Auxiliary File Standard

For decades, a set of common practices has evolved that developers of user
applications for POSIX/Unix platforms providing fair portability, easily
discoverable structure, modularity, and convenience for both developers and
users.  These common practices have not been defined by a formalized standard,
but a de facto standard has arisen as an emergent phenomenon over a period of
decades.  This de facto standard generally possesses the following
characteristics:

* traditional

* well understood

* fairly simple to implement and use

* modular

* discoverable

* portable

It also does not tend to fall prey to problems like littering your filesystem
hierarchy with infrastructural directory paths whose only purpose is to
maintain compliance with the standard, nor does it invade directories designed
to manage data and configuration files for core system components with data and
configuration files that serve the purposes of user level applications that may
come and go over time, quickly making those directories more difficult to
manage.

This de facto standard has had precisely three problems:

1. Many people are not aware of it, because it has not been described in a
   formal specification before this.

2. It competes with alternatives that enjoy the social benefits of formalized
   standardization for mindshare amongst the members of a standards-conscious
   community of developers.

3. There are people who do not use it.

## Rationale

Rather than develop a new standard, it is preferable to simply establish a
formal specification to describe a suitable standard that already (informally)
exists.  This project is an attempt to do so, and to support the development of
standardized tools to automate management of auxiliary file defaults.  With
effective advocacy and conscientious stewardship, the result of this project
should be the solution to problems 1 and 2.  There is no known cure for ailment
3, and it is an affliction common to standards and specifications of all
stripes.

## Conclusion

> SHAFD is a bad mother . . .
>
> "Shut yo' mouf!"
>
> I'm just talkin' 'bout SHAFD.
>
> "We can dig it!"
