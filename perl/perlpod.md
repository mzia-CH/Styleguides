# Perl POD Documentation Standards

## 1. Introduction
This document outlines key practices for writing clean and efficient Perl code.
It is based on the [official perlpod docs](https://perldoc.perl.org/perlpod).

### 1.1 **Why Use Pod?**
`Pod` is a simple-to-use markup language specifically designed for Perl documentation. It offers:
- **Ease of Formatting:** Convert to plain text, HTML, man pages, and more.
- **Consistency:** Standard structure makes it easier to write and read.
- **Integration:** Embed directly into Perl modules and scripts, keeping documentation close to the code.
- **Portability:** `Pod`-formatted documentation can be transformed into multiple formats, making it easy to distribute.
- **Standardization:** New developers familiar with Perl will already recognize `Pod` syntax, reducing the learning curve.

---

## 2. Documentation Guidelines

### 2.1 **Pod Structure Basics**
Pod documents consist of three main paragraph types:

- **Ordinary Paragraphs:** Regular text blocks with minimal formatting.
- **Verbatim Paragraphs:** Pre-formatted blocks (code snippets) using leading whitespace.
- **Command Paragraphs:** Special commands for headings, lists, and formatting.

### 2.2 **Pod Commands and Syntax**
Use the following commands to structure your documentation clearly and consistently:

### 2.3 **Headings**
Use headings to organize the documentation hierarchy and improve readability.
```perl
=head1 Main Title
=head2 Subsection
=head3 Sub-subsection
```
✅ **Tip:** `=head1` is the highest-level heading; use `=head2`, `=head3`, etc., for subsections. Use consistent casing and formatting for readability.

### 2.4 **Lists**
Create bullet-point or numbered lists using `=over`, `=item`, and `=back` commands.

**Example:**
```perl
=over 4

=item * First item

=item * Second item

=back
```
✅ Use `=item 1.`, `=item 2.` for numbered lists.

### 2.5 **Code Blocks (Verbatim)**
For pre-formatted text (code examples), start the paragraph with whitespace (space or tab).
```perl
    my $variable = 10;
    print "$variable\n";
```
✅ Indentation is preserved and rendered as preformatted text.

### 2.6 **Links**
Reference Perl modules, sections, or external links.
```perl
L<Perl Documentation|https://perldoc.perl.org>
L<SomeModule::Name>
```
✅ Use `L<text|url>` for external links and `L<Module::Name>` for internal references.

### 2.7 **Formatting Codes**
Use these codes for inline formatting:
- `B<bold>` → **bold**
- `I<italic>` → *italic*
- `C<code>` → `code` text
- `F<filename>` → filename style

✅ Example:
```perl
B<Important>: Use C<strict> and C<warnings> in your code.
```

### 2.8 **Escaping Special Characters**
To include special characters such as `=` or `>` without being interpreted as Pod commands, use the `E<>` escape sequence:
```perl
E<gt>   # Greater than (>)
E<lt>   # Less than (<)
E<equals> # Equals sign (=)
```

---

## 3. Documentation Conventions

### 3.1 **Headers and Sections**
Use clear section headings to structure the content. Follow this format:

```perl
=head1 NAME
My::Module - Brief module description

=head1 SYNOPSIS
Example usage of the module.

=head1 DESCRIPTION
Detailed description of the module's functionality.

=head1 METHODS
Document the key methods with parameters and return values.

=head1 AUTHOR
Your Name <email@domain.com>
```
✅ Always include `NAME`, `SYNOPSIS`, and `DESCRIPTION` sections for consistency and readability.

### 3.2 **Consistent Formatting and Style**
- Use `=head1` for main sections, `=head2` for subsections, and `=head3` for minor subsections.
- Separate paragraphs with a blank line for clarity.
- Use consistent indentation for verbatim blocks.
- Use `=cut` to end Pod blocks cleanly.
- Include clear and meaningful comments in the code blocks to explain functionality.

---

## 4. Embedding Pod in Perl Code

### 4.1 **Basic Embedding**
Embed documentation directly into Perl scripts using Pod blocks.
```perl
#!/usr/bin/perl
use strict;
use warnings;

=head1 NAME
MyScript - Example script

=cut

print "Hello, Perl!\n";
```
✅ Keep documentation blocks close to the related code for easy reference.

### 4.2 **In-Module Documentation**
Document modules with clear sections and usage examples.
```perl
package My::Module;

=head1 NAME
My::Module - Example module

=head1 DESCRIPTION
This module performs example operations.

=head1 METHODS

=head2 new()
Creates a new object.

=cut

sub new {
    my $class = shift;
    return bless {}, $class;
}
```
✅ Use `=cut` to return to the Perl code after documentation blocks.

---

## 5. Examples and Best Practices

### 5.1 **Consistent Code Examples**
Use clear, complete code snippets with context to ensure readability.

✅ **Good example:**
```perl
=head2 Using the Module

Example usage:

    use My::Module;
    my $obj = My::Module->new();
```

❌ **Bad example:**
```perl
use Module; # Missing context and explanation
```

### 5.2 **Descriptive Method Documentation**
Clearly describe method behavior, parameters, and return values for better clarity.

✅ Example:
```perl
=head2 add_numbers($a, $b)

Adds two numbers and returns the sum.

Parameters:
    $a - First number
    $b - Second number

Returns:
    Sum of $a and $b.
```

### 5.3 **Private Methods**
Use `##` comments for private methods and include `@param` and `@returns` tags for consistency.

✅ Example:
```perl
## [void] _myPrivateMethod($param1)
#
#   @param  param1   [string]   input value
#
sub _myPrivateMethod {
    my ($self, $param1) = @_;
    ...
}
```

---

## 6. Validation and Linting
Use `podchecker` to validate Pod syntax and catch errors.

```bash
podchecker yourfile.pod
```
✅ Check for missing blank lines, invalid commands, and unrecognized formatting codes.

---

## 7. Staying Consistent
Following these Pod standards ensures your Perl documentation is clear, consistent, and easy to maintain. Always:
- Use proper headings, lists, and formatting codes.
- Embed documentation in modules and scripts.
- Validate with `podchecker` to catch errors.


