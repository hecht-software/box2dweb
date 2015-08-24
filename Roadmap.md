# Roadmap #

Planned features and improvements for the next major release:

  * ~~Support Windows Internet Explorer versions 8 and 9~~ ([issue #12](https://code.google.com/p/box2dweb/issues/detail?id=#12), [r21](https://code.google.com/p/box2dweb/source/detail?r=21); version 8 won't be supported. Please notify me, if your opinion is that IE8 support is important.)
  * ~~Replace "for/in" by "for" when traversing arrays~~ ([issue #13](https://code.google.com/p/box2dweb/issues/detail?id=#13), [r24](https://code.google.com/p/box2dweb/source/detail?r=24))
  * Replace b2Vec2 by WebGL arrays internally (Fall back if WebGL is not available)
  * Reduce function calls
  * Reduce references
  * Improve minification by evaluating "private" and "public" modificators
  * Keep documentation comments in the non-minified source code
  * Replace properties by methods
  * Provide an own API-documentation

# How about a hand-written port of Box2dFlash? #

There are some reasons why I don't like the idea of converting Box2dFlash using a compiler anymore.
Box2dFlash shows no activities since I started writing my converter. Their version still is in an alpha-state. The main reason why I decided to write a converter was to easily keep my port up to date.
After finishing my work and using the port I realized some bad things about Box2dFlash. E.g. debug drawing is implemented in a bad way. Parts of the drawing code are defined in b2World and b2Controller, whereas Box2D only provides debug drawing in the external test-bed.
Furthermore, they are iterating through arrays using for/in at many places which leads to performance problems.

So, why not creating a new port by hand?

I considered to do this, but there are some problems with this idea as well.
Javascript doesn't support types and modificators like "public" and "private". I think that these informations play an important role for optimizations. For instance, I'm able to define a namespace "b2Inline" and make the converter processing inline functions. In Javascript you have to copy-and-paste code if you want to inline functions in order to improve performance.

So, what should I do, instead?

I have no concrete plans, but if I write a port by hand, then it will be a C++ to ActionScript port. As for the Javascript version, I'll use my converter again.