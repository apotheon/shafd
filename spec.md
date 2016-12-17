# Working Specification Document

## Terminology

The term "tool" will be used to refer to the software whose auxiliary files may
be addressed in any explanations or examples.

## Auxiliary File Defaults

At present, this specification is "in-progress", and its recommendations may
change as expansion and refinement continues.  Use at your own risk.

### User Directories

Standard/default location for user-specific auxiliary files should be in a
tool-specific dot-directory named after the tool (e.g. `.foo` directory for the
`foo` tool).  Some exceptions may apply.

Datafiles shared across different, fully distinct tools may be stored in a
single directory.  When the only tools that may make use of the datafiles other
than the tool whose auxiliary datafiles conform to this specification are
support tools for that primary tool, this exception does not apply.

Configuration files shared across different, fully distinct tools may be stored
in a single directory.  This directory should be the `~/.config` directory.
When the only tools that may make use of the configuration files other than the
tool whose auxiliary configuration files conform to this specification are
support tools for that primary tool, this exception does not apply.

Tools that may require configuration files but, by their particular nature, do
not require any other auxiliary files and the configuration files are
necessarily managed in an automated fashion with no expectation of human
intervention may store their configuration files in a single directory.  This
directory should be a tool-specific subdirectory of `~/.config`.

### System Directories

Standard/default location for system-wide auxiliary files should be in a
tool-specific . . .
