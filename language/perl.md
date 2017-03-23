<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [perl in basic commond line edit](#perl-in-basic-commond-line-edit)
- [EOC](#eoc)
- [perl little trick](#perl-little-trick)
  - [// operator](#-operator)
  - [... yada yada](#-yada-yada)
  - [-> and autobox](#--and-autobox)
  - [s///r](#sr)
  - [here doc and inline file](#here-doc-and-inline-file)
  - [q, qq, and qw notation](#q-qq-and-qw-notation)
- [system](#system)
- [opts](#opts)
- [is pid running](#is-pid-running)
- [Data::Dumper](#datadumper)
- [Test::LongString](#testlongstring)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

---
title: "perl note"
date: 2016-06-30 08:00
---
[TOC]

### perl in basic commond line edit

perldoc perlrun


```
cat a.html | perl -p -e 's/a/b/g' > b.html
```
```
-e: Allows you to provide the program as an argument rather
    than in a file. You don't want to have to create a script
    file for every little Perl one-liner.
-i: Modifies your input file in-place (making a backup of the
    original). Handy to modify files without the {copy,
    delete-original, rename} process.
-w: Activates some warnings. Any good Perl coder will use this.
-d: Runs under the Perl debugger. For debugging your Perl code,
    obviously.
-t: Treats certain "tainted" (dubious) code as warnings (proper
    taint mode will error on this dubious code). Used to beef
    up Perl security, especially when running code for other
    users, such as setuid scripts or web stuff.
```

### EOC
perl provide pipe like feature, we can use this feature like template.

```
  print $out <<_EOC_;
$html_comment
<html>
 <head>
  <title>$infile - $pkg_name</title>
  <meta http-equiv="Content-Type" content="text/html;charset=$charset">
  <style>
$css
  </style>
 </head>
 <body>
$nav
  <h1>$infile - $pkg_name</h1>
$preamble
  <code>$src</code>
$nav
 </body>
</html>
_EOC_
```


### perl little trick 

#### // operator

```
$home =  $ENV{HOME}
	  // $ENV{LOGDIR}
	  // (getpwuid($<))[7]
	  // die "You're homeless!\n";
```

#### ... yada yada

```
sub unimplemented {
    ...
}
```


#### -> and autobox

$hash->{key} 

#### s///r

```
$x = "I like dogs.";
$y = $x =~ s/dogs/cats/r;
print "$x $y\n"; # prints "I like dogs. I like cats."
```


#### here doc and inline file
```
my $str = <<__;
some string here
bla blah
__

```

```
while( <DATA> ) {
    print;
}
__DATA__
file content
```


#### q, qq, and qw notation
q : literal quote; only character that needs to be escaped is the end character  
```
my $var3 = q(Others prefer parens as the quote mechanism.);

```
qq : an interpreted quote; processes variables and escape characters. Great for strings that you need to quote:  

```
my $var4 = qq{This "$mechanism" is broken.  Please inform "$user" at "$email" about it.};
```

qx : Works like qq, but then executes it as a system command, non interactively. Returns all the text generated from the standard out.
```
my $moreout = qx{type "$path" 2>&1}; # get stuff on stderr too
```
qr : Interprets like qq, but then compiles it as a regular expression. Works with the various options on the regex as well. You can now pass the regex around as a variable:

```
sub MyRegexCheck {
    my ($string, $regex) = @_;
    if ($string)
    {
       return ($string =~ $regex);
    }
    return; # returns 'null' or 'empty' in every context
}

my $regex = qr{http://[\w]\.com/([\w]+/)+};
@results = MyRegexCheck(q{http://myurl.com/subpath1/subpath2/}, $regex);

```

qw : A very, very useful quote operator. Turns a quoted set of whitespace separated words into a list.

```
my @badwords = qw(WORD1 word2 word3 word4);

my @list = ('string with space', qw(eight nine), "a $var"); # works in other lists
```


### system
```
if ($^O ne 'linux') {
    die "Only linux is supported but I am on $^O.\n";
}
```

### opts

```
getopts("a:dhl:p:t:uk", \%opts)
or die usage();

if ($opts{h}) {
    print usage();
    exit;
}

my $pid = $opts{p}
or die "No process pid specified by the -p option.\n";

```

### is pid running

```
my $exec_file = "/proc/$pid/exe";
if (!-f $exec_file) {
    die "Nginx process $pid is not running or ",
	"you do not have enough permissions.\n";
}
```


### Data::Dumper

```
use Data::Dumper;
@ll = ("hello","world");
print Dumper(@ll);
```

### Test::LongString 
test::longstring can use for differ string.



