# Introduction #

For basic usage of Box2D, you should read the documentation of the original C++ version: http://www.box2d.org/manual.html

Box2dWeb is organized the same way as Box2dFlash. I.e. the API is almost identical. You can find the documentation here:
http://www.box2dflash.org/docs/2.1a/reference/

Anyways, there are some differences which are documented on this page.

# Importing Classes #

There is no way to import packages and classes in Javascript, so you have to use var assignments, if you don't want to use full addresses.

The code below demonstrates my recommendation how to write Javascript in general, because the global scope is not polluted. This increases performance, because the Javascript engine doesn't need to traverse the whole scope-chain when looking up your definitions. It also contains the assignments which are most commonly used when starting a new project, so you can copy and paste it.

```
(function() {

   var b2Vec2 = Box2D.Common.Math.b2Vec2;
   var b2BodyDef = Box2D.Dynamics.b2BodyDef;
   var b2Body = Box2D.Dynamics.b2Body;
   var b2FixtureDef = Box2D.Dynamics.b2FixtureDef;
   var b2Fixture = Box2D.Dynamics.b2Fixture;
   var b2World = Box2D.Dynamics.b2World;
   var b2MassData = Box2D.Collision.Shapes.b2MassData;
   var b2PolygonShape = Box2D.Collision.Shapes.b2PolygonShape;
   var b2CircleShape = Box2D.Collision.Shapes.b2CircleShape;
   var b2DebugDraw = Box2D.Dynamics.b2DebugDraw;
   

})();
```

# Debug Drawing #

Although Box2D is a physics engine and therefore has nothing to do with drawing, Box2dFlash provides such methods for debugging which are defined in the b2DebugDraw class.
In Box2dWeb, a _b2DebugDraw_ takes a canvas-context instead of a Sprite:

```
var debugDraw = new Box2D.Dynamics.b2DebugDraw;
debugDraw.SetSprite(document.GetElementsByTagName("canvas")[0].getContext("2d"));
```


# Working with Events #

You have to implement event-interfaces in Box2dFlash. Since Javascript doesn't support classical inheritance natively, I show you how to deal with events in Box2dWeb:

```
var world = new Box2D.Dynamics.b2World(new Box2d.Common.Math.b2Vec2(0, 10), true);

/* ... add bodies, etc. ... */

var myListener = new Box2D.Dynamics.b2DestructionListener;

myListener.SayGoodbyeFixture = function(fixture) {
   alert("goodbye fixture ...");
}

world.SetDestructionListener(myListener);
```