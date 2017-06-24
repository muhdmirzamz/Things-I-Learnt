## SpriteKit

- Just giving `collisionBitMask` a value will automatically apply physics to an object. Default behaviour is to bounce off collided objects.
- `contactTestBitMask` will **notify** you of the collision/contact. Adopt the `SKPhysicsContactDelegate` to your scene class, set the `contactDelegate` and implement the delegate methods to customise what happens when there's contact between two physics bodies.
- The preferred order in `SpriteKit` is to 
- This is an example showing how to make the scene's frame a border so other physics bodies won't go beyond it.
``` swift
let borderBody = SKPhysicsBody.init(edgeLoopFrom: self.frame)
self.physicsBody = borderBody
self.physicsBody?.categoryBitMask = Collision.Block
self.physicsBody?.collisionBitMask = Collision.Player
```
