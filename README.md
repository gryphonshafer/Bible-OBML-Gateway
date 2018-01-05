# NAME

Bible::OBML::Gateway - Bible Gateway content conversion to Open Bible Markup Language (OBML)

# VERSION

version 1.02

[![Build Status](https://travis-ci.org/gryphonshafer/Bible-OBML-Gateway.svg)](https://travis-ci.org/gryphonshafer/Bible-OBML-Gateway)
[![Coverage Status](https://coveralls.io/repos/gryphonshafer/Bible-OBML-Gateway/badge.png)](https://coveralls.io/r/gryphonshafer/Bible-OBML-Gateway)

# SYNOPSIS

    use Bible::OBML::Gateway;

    my $bg = Bible::OBML::Gateway->new;
    $bg->translation('NIV');

    my $obml = $bg->get( 'Romans 12', 'NIV' )->obml;
    my $data = $bg->get( 'Romans 12' )->data;
    my $html = $bg->get('Romans 12')->html;

    $bg->get( 'Romans 12', 'NIV' )->save('Romans_12_NIV.html');
    say $bg->load('Romans_12_NIV.html')->obml;

# DESCRIPTION

This module consumes Bible Gateway content and converts it to Open Bible Markup
Language (OBML).

# METHODS

The following methods are supported.

## new

Instantiates a new gateway object. You can optionally pass a translation
acronym to be used on subsequent requests.

    my $bg = Bible::OBML::Gateway->new('NIV');

## translation

Get or set the current translation acronym.

    say $bg->translation;
    $bg->translation('NIV');

## get

Gets the raw HTML content for a given chapter represented by book, chapter,
and translation. The book and chapter can be combined with a space. The
translation if provided will override the translation set in the object.

    $bg->get( 'Romans 12', 'NIV' );
    $bg->get('Romans 12');

## obml

Parses the previously `get()`-ed raw HTML if it hasn't been parsed yet and
returns Open Bible Markup Language (OBML) using [Bible::OBML](https://metacpan.org/pod/Bible::OBML).

    my $obml = $bg->get('Romans 12')->obml;

## data

Parses the previously `get()`-ed raw HTML if it hasn't been parsed yet and
returns a data structure of content that could be passed into [Bible::OBML](https://metacpan.org/pod/Bible::OBML)'s
`render()` method.

    my $data = $bg->get('Romans 12')->data;

## html

Returns the previously `get()`-ed raw HTML.

    my $html = $bg->get('Romans 12')->html;

## save

Saves the previously `get()`-ed raw HTML to a file.

    $bg->get('Romans 12')->save('Romans_12_NIV.html');

## load

Loads raw HTML from a file.

    say $bg->load('Romans_12_NIV.html')->obml;

# SEE ALSO

[Bible::OBML](https://metacpan.org/pod/Bible::OBML), [Bible::OBML::HTML](https://metacpan.org/pod/Bible::OBML::HTML), [Bible::Reference](https://metacpan.org/pod/Bible::Reference).

You can also look for additional information at:

- [GitHub](https://github.com/gryphonshafer/Bible-OBML-Gateway)
- [CPAN](http://search.cpan.org/dist/Bible-OBML-Gateway)
- [MetaCPAN](https://metacpan.org/pod/Bible::OBML::Gateway)
- [AnnoCPAN](http://annocpan.org/dist/Bible-OBML-Gateway)
- [Travis CI](https://travis-ci.org/gryphonshafer/Bible-OBML-Gateway)
- [Coveralls](https://coveralls.io/r/gryphonshafer/Bible-OBML-Gateway)
- [CPANTS](http://cpants.cpanauthors.org/dist/Bible-OBML-Gateway)
- [CPAN Testers](http://www.cpantesters.org/distro/B/Bible-OBML-Gateway.html)

# AUTHOR

Gryphon Shafer <gryphon@cpan.org>

# COPYRIGHT AND LICENSE

This software is copyright (c) 2018 by Gryphon Shafer.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
