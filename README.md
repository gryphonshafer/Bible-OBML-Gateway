# NAME

Bible::OBML::Gateway - Bible Gateway content conversion to Open Bible Markup Language

# VERSION

version 2.03

[![test](https://github.com/gryphonshafer/Bible-OBML-Gateway/workflows/test/badge.svg)](https://github.com/gryphonshafer/Bible-OBML-Gateway/actions?query=workflow%3Atest)
[![codecov](https://codecov.io/gh/gryphonshafer/Bible-OBML-Gateway/graph/badge.svg)](https://codecov.io/gh/gryphonshafer/Bible-OBML-Gateway)

# SYNOPSIS

    use Bible::OBML::Gateway;

    my $bg = Bible::OBML::Gateway->new;
    $bg->translation('NIV');

    my $obml_obj = $bg->get( 'Romans 12' );
    print $bg->get( 'Romans 12', 'NASB' )->obml, "\n";

    my $translations = $bg->translations;
    my $structure    = $bg->structure('NASB');

# DESCRIPTION

This module consumes Bible Gateway content and returns useful data-bearing
objects or data structures. In the common case, it will accept a Bible reference
and return a [Bible::OBML](https://metacpan.org/pod/Bible%3A%3AOBML) object loaded with parsed content.

# METHODS

The following methods are supported.

## new

Instantiates a new gateway object. You can optionally pass a translation
acronym to be used on subsequent requests.

    my $bg = Bible::OBML::Gateway->new( translation => 'NIV' );

## get

This method requires a text input containing a Bible reference that can be
understood as a single chapter or single, unbroken run of verses. For example,
"Romans 12" or "Ro 12:13-17" are acceptable, but "Romans 12:13-17, 19" is not.

You can optionally also provide an overriding translation. If not specified,
the object's translation (set via the `translation` attribute) will be used.

The method will get the raw HTML content from Bible Gateway, parse it, and
return a [Bible::OBML](https://metacpan.org/pod/Bible%3A%3AOBML) object loaded with the data.

    my $obml_obj = $bg->get( 'Romans 12' );
    print $bg->get( 'Romans 12', 'NASB' )->obml, "\n";

Internally, all this method does is call `fetch`, pass that output to `parse`,
and then load output that into a new [Bible::OBML](https://metacpan.org/pod/Bible%3A%3AOBML) object.

## fetch

If all you want to do is fetch the HTML from Bible Gateway, you can use this
method. It uses the same signature as `get` and returns the returned raw HTML.

## parse

This method requires source HTML like what you might get from a `fetch` call,
which it will then parse and return a special sort of HTML that can be loaded
directly into a [Bible::OBML](https://metacpan.org/pod/Bible%3A%3AOBML) object via it's `html` method. (See
[Bible::OBML](https://metacpan.org/pod/Bible%3A%3AOBML) for more information.)

## translations

This method will return a data structure consisting of data describing available
translations on Bible Gateway per spoken language. It returns an arrayref
containing a hashref per language. Each hashref contains an arrayref of
translations, each represented by a hashref.

    my $translations = $bg->translations;

This a simplified example of the data structure:

    [
        {
            acronym      => 'EN',
            language     => 'English',
            translations => [
                {
                    acronym     => 'NIV',
                    translation => 'New International Version',
                },
            ],
        },
    ]

## structure

This method will return a data structure consisting of data describing the
structure of a given translation of the Bible from Bible Gateway. It can
optionally be provided an overriding translation. If not specified, the object's
translation (set via the `translation` attribute) will be used. The data
structure returned is an arrayref of hashrefs, each representing a book.

    my $structure = $bg->structure('NASB');

This a simplified example of the data structure:

    [
        {
            testament    =>  'NT',
            display      =>  '2 John',
            osis         =>  '2John',
            intro        =>  0,
            num_chapters =>  1,
            chapters     =>  [
                {
                    chapter => 1,
                    type    => 'heading',
                    content => [
                        "Walk According to His Commandments",
                    ],
                },
            ],
        }
    ]

# ATTRIBUTES

Attributes can be set in a call to `new` or explicitly as a get/set method.

    my $bg = Bible::OBML::Gateway->new( translation => 'NIV' );
    $bg->translation('NIV');
    say $bg->translation;

## translation

Get or set the current translation acronym. The default if not explicitly set
will be "NIV".

    say $bg->translation;
    $bg->translation('NIV');

## url

This provides access to the base URL, contained within a [Mojo::URL](https://metacpan.org/pod/Mojo%3A%3AURL) object.

    $bg->url( Mojo::URL->new('https://www.biblegateway.com/passage/') );

## ua

This provides access to the [Mojo::UserAgent](https://metacpan.org/pod/Mojo%3A%3AUserAgent) user agent.

    $bg->ua->transactor->name("Your Application's Name");

## reference

This provides access to the [Bible::Reference](https://metacpan.org/pod/Bible%3A%3AReference) object used to parse and
canonicalize Bible references.

    $bg->reference->bible('Catholic');

Depending on which translation you `get` from Bible Gateway, you may need to
alter the `bible` setting of `reference`, as in the example immediately above.
By default, `bible` is set to "Protestant".

# SEE ALSO

[Bible::OBML](https://metacpan.org/pod/Bible%3A%3AOBML), [Bible::Reference](https://metacpan.org/pod/Bible%3A%3AReference), [Mojo::URL](https://metacpan.org/pod/Mojo%3A%3AURL), [Mojo::UserAgent](https://metacpan.org/pod/Mojo%3A%3AUserAgent).

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

This software is Copyright (c) 2017-2050 by Gryphon Shafer.

This is free software, licensed under:

    The Artistic License 2.0 (GPL Compatible)
