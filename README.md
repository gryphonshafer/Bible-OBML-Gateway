# NAME

Bible::OBML::Gateway - Bible Gateway content conversion to Open Bible Markup Language (OBML)

# VERSION

version 1.12

[![test](https://github.com/gryphonshafer/Bible-OBML-Gateway/workflows/test/badge.svg)](https://github.com/gryphonshafer/Bible-OBML-Gateway/actions?query=workflow%3Atest)
[![codecov](https://codecov.io/gh/gryphonshafer/Bible-OBML-Gateway/graph/badge.svg)](https://codecov.io/gh/gryphonshafer/Bible-OBML-Gateway)

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

    my $bg = Bible::OBML::Gateway->new( translation => 'NIV' );

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
returns Open Bible Markup Language (OBML) using [Bible::OBML](https://metacpan.org/pod/Bible%3A%3AOBML).

    my $obml = $bg->get('Romans 12')->obml;

## data

Parses the previously `get()`-ed raw HTML if it hasn't been parsed yet and
returns a data structure of content that could be passed into [Bible::OBML](https://metacpan.org/pod/Bible%3A%3AOBML)'s
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

[Bible::OBML](https://metacpan.org/pod/Bible%3A%3AOBML), [Bible::OBML::HTML](https://metacpan.org/pod/Bible%3A%3AOBML%3A%3AHTML), [Bible::Reference](https://metacpan.org/pod/Bible%3A%3AReference).

You can also look for additional information at:

- [GitHub](https://github.com/gryphonshafer/Bible-OBML-Gateway)
- [MetaCPAN](https://metacpan.org/pod/Bible::OBML::Gateway)
- [GitHub Actions](https://github.com/gryphonshafer/Bible-OBML-Gateway/actions)
- [Codecov](https://codecov.io/gh/gryphonshafer/Bible-OBML-Gateway)
- [CPANTS](http://cpants.cpanauthors.org/dist/Bible-OBML-Gateway)
- [CPAN Testers](http://www.cpantesters.org/distro/B/Bible-OBML-Gateway.html)

# AUTHOR

Gryphon Shafer <gryphon@cpan.org>

# COPYRIGHT AND LICENSE

This software is Copyright (c) 2017-2021 by Gryphon Shafer.

This is free software, licensed under:

    The Artistic License 2.0 (GPL Compatible)
