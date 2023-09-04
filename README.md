# NAME

Acme::Glue - A placeholder module for code accompanying a Perl photo project

# VERSION

2023.10

# DESCRIPTION

Acme::Glue is the companion Perl module for a Perl photo project, the idea
for the photo project is to have each photo include a small snippet of code.
The code does not have to be Perl, it just has to be something you're quite
fond of for whatever reason.

"Glue" is a series of photos shot at Perl conferences and workshops in Europe
and America. Perl was one of the programming languages that bootstrapped a
lot of internet based companies in the mid/late 1990s and early 2000s. Perl
was considered a “glue” language by some, but has fallen out of favour as
newer languages have taken its place. The title is a metaphor not just for
the language but also for shrinking of the community at the events the photos
are shot at.

# SNIPPETS

Here are the snippets that may accompany the photo project

## LEEJO (transform.pl)

    #!/usr/bin/env perl
    #
    # transform an array of hashes into an array of arrays where each array
    # contains the values from the hash sorted by the original hash keys or
    # the passed order of columns (hash slicing)
    my @ordered = $column_order
        ? map { [ @$_{ @{ $column_order } } ] } @{ $chaos }
        : map { [ @$_{sort keys %$_} ] } @{ $chaos };

## LEEJO (hopscotch.p6)

    #!/usr/bin/env perl6

    my @court = (
        [ 'FIN' ],
        [ 9 ,10 ],
        [   8   ],
        [ 6 , 7 ],
        [   5   ],
        [   4   ],
        [ 2 , 3 ],
        [   1   ],
    );

    my $skip = @court.[1..*].pick.pick;
    my @play;

    for @court.reverse -> $hop {
        @play.push( $hop.map( *.subst( /^$skip$/,'🚫' ).list ) );
    }

    say @play.reverse.join( "\n" );

## LEEJO (vec and pack examples from perldoc vec)

    #!/usr/bin/env perl -wl

    print <<'EOT';
                                      0         1         2         3
                       unpack("V",$_) 01234567890123456789012345678901
    ------------------------------------------------------------------
    EOT

    for $w (0..3) {
        $width = 2**$w;
        for ($shift=0; $shift < $width; ++$shift) {
            for ($off=0; $off < 32/$width; ++$off) {
                $str = pack("B*", "0"x32);
                $bits = (1<<$shift);
                vec($str, $off, $width) = $bits;
                $res = unpack("b*",$str);
                $val = unpack("V", $str);
                write;
            }
        }
    }

    format STDOUT =
    vec($_,@#,@#) = @<< == @######### @>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
    $off, $width, $bits, $val, $res
    .
    __END__

## LEEJO (example from "How Perl Saved the Human Genome Project" complete with syntax error)

    use Boulder::Stream; 
    $stream = new Boulder::Stream; 
    while ($record=$stream->read_record('NAME','SEQUENCE')) {
        $name = $record->get('NAME'); 
        $sequence = $record->get('SEQUENCE'); 

        ...continue processing...

        $record->add(QUALITY_CHECK=>"OK|); 
        $stream->write_record($record); 
    } 

## LEEJO (quine - a program that prints itself out)

    $_=q(print"\$_=q($_);eval;");eval;

## LEEJO (perl5 LOC count as of 5.38 release)

    % git branch
    * blead
    % find . -name "*.[ch]" | xargs wc -l | sort -nr | head -n5
      788279 total
      436086 ./charclass_invlists.h
       17540 ./sv.c
       16254 ./regcomp.c
       15712 ./op.c

## MIKESTOK (soundex "joke")

    sub Soundex
    {
      local ($_, $f) = shift;

      y;a-z;A-Z;;y;A-Z;;cd;$_ ne q???do{($f)=m;^(.);;s;$f+;;;
      y;AEHIOUWYBFPVCGJKQSXZDTLMNR;00000000111122222222334556;;
      y;;;cs;y;0;;d;s;^;$f;;s;$;0000;;m;(^.{4});;$1;}:q;;;
    }

## NERDVANA (delorean\_ options.pl)

    GetOptions(
        'help|h|?'       => sub { pod2usage(1) },
        'serial-dev|d=s' => \my $opt_serial_dev= '/dev/delorean',
        'socket|S=s'     => \my $opt_socket= '/run/uctl-daemon.sock',
    ) or pod2usage(2);

## SLU (MAZE.BAS)

    10 PRINT CHR$(205.5+RND(1));:GOTO 10

## SLU (schwartzian\_transform.pl)

    #!/usr/bin/env perl
    # https://en.wikipedia.org/wiki/Schwartzian_transform
    # Sort list of words according to word length

    print "$_\n" foreach
      map  { $_->[0] }
      sort { $a->[1] <=> $b->[1] or $a->[0] cmp $b->[0] }
      map  { [$_, length($_)] }
      qw(demo of schwartzian transform);

# THANKS

Thanks to all who contributed a snippet

# SEE ALSO

[https://www.formulanon.com/glue](https://www.formulanon.com/glue)

[https://www.youtube.com/watch?v=ir6f2SvsXPA&feature=youtu.be&list=PLOOlhkMvt\_o4y627mpaCGrO4ughSEeUgb&t=1046](https://www.youtube.com/watch?v=ir6f2SvsXPA&feature=youtu.be&list=PLOOlhkMvt_o4y627mpaCGrO4ughSEeUgb&t=1046)

[https://leejo.github.io/acme-glue-talk/presentation.html#1](https://leejo.github.io/acme-glue-talk/presentation.html#1)

# AUTHOR

Lee Johnson - `leejo@cpan.org`

# LICENCE

This library is free software; you can redistribute it and/or modify it under
the same terms as Perl itself. If you would like to contribute documentation,
features, bug fixes, or anything else then please raise an issue / pull request:

    https://github.com/leejo/acme-glue

All photos © Lee Johnson
