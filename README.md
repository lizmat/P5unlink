NAME
====

Raku port of Perl's unlink() built-in

SYNOPSIS
========

    use P5unlink;

    say unlink("foobar"); # 1 if successful, 0 if not

    with "foobar" {
        say unlink; # 1 if succesful, 0 if not
    }

    say unlink(@paths); # number of files removed

DESCRIPTION
===========

This module tries to mimic the behaviour of Perl's `unlink` built-in as closely as possible in the Raku Programming Language.

ORIGINAL PERL DOCUMENTATION
===========================

    unlink LIST
    unlink  Deletes a list of files. On success, it returns the number of
            files it successfully deleted. On failure, it returns false and
            sets $! (errno):

                my $unlinked = unlink 'a', 'b', 'c';
                unlink @goners;
                unlink glob "*.bak";

            On error, "unlink" will not tell you which files it could not
            remove. If you want to know which files you could not remove,
            try them one at a time:

                 foreach my $file ( @goners ) {
                     unlink $file or warn "Could not unlink $file: $!";
                 }

            Note: "unlink" will not attempt to delete directories unless you
            are superuser and the -U flag is supplied to Perl. Even if these
            conditions are met, be warned that unlinking a directory can
            inflict damage on your filesystem. Finally, using "unlink" on
            directories is not supported on many operating systems. Use
            "rmdir" instead.

            If LIST is omitted, "unlink" uses $_.

PORTING CAVEATS
===============

removing directories *not* supported
------------------------------------

As the original documents indicate, use `rmdir` instead.

$_ no longer accessible from caller's scope
-------------------------------------------

In future language versions of Raku, it will become impossible to access the `$_` variable of the caller's scope, because it will not have been marked as a dynamic variable. So please consider changing:

    unlink;

to either:

    unlink($_);

or, using the subroutine as a method syntax, with the prefix `.` shortcut to use that scope's `$_` as the invocant:

    .&unlink;

AUTHOR
======

Elizabeth Mattijsen <liz@raku.rocks>

If you like this module, or what I’m doing more generally, committing to a [small sponsorship](https://github.com/sponsors/lizmat/) would mean a great deal to me!

Source can be located at: https://github.com/lizmat/P5unlink . Comments and Pull Requests are welcome.

COPYRIGHT AND LICENSE
=====================

Copyright 2023 Elizabeth Mattijsen

Re-imagined from Perl as part of the CPAN Butterfly Plan.

This library is free software; you can redistribute it and/or modify it under the Artistic License 2.0.

