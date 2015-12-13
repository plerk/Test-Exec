# Test::Exec [![Build Status](https://secure.travis-ci.org/plicease/Test-Exec.png)](http://travis-ci.org/plicease/Test-Exec)

Test that some code calls exec without terminating testing

# SYNOPSIS

    use Test::More;
    use Test::Exec;
    
    is_deeply exec_arrayref { exec 'foo', 'bar', 'baz' }, [qw( foo bar baz )], 'found exec!';
    is exec_arrayref { }, undef, 'did not exec!';

# DESCRIPTION

[Test::Exec](https://metacpan.org/pod/Test::Exec) provides the most simple possible tools for testing code that might call `exec`, which
would otherwise end your test by calling another program.  This code should detect and capture `exec`
calls, even if they are inside an `eval`.

The concept was implementation was based on [Test::Exit](https://metacpan.org/pod/Test::Exit), but applied to `exec` instead of `exit`.

# FUNCTIONS

## exec\_arrayref

    exec_arrayref { ... }

runs the given code.  If the code calls `exec`, then this function will return an arrayref with its
arguments.  If the code never calls `exec`, it will return `undef`.

# CAVEATS

This module installs its own version of `exec` in `CORE::GLOBAL::exec`,
and may interact badly with any other code that is also trying to do
such things.

# SEE ALSO

- [Test::Exit](https://metacpan.org/pod/Test::Exit)

    Very similar to (and inspired) this module, but for `exit` testing instead of `exec`.

- [Test::Mock::Cmd](https://metacpan.org/pod/Test::Mock::Cmd)

    Provides an interface to mocking `system`, `qx` and `exec`.

# AUTHOR

Graham Ollis &lt;plicease@cpan.org>

# COPYRIGHT AND LICENSE

This software is copyright (c) 2015 by Graham Ollis.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
