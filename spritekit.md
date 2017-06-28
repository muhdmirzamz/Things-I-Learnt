## SpriteKit

- Just giving `collisionBitMask` a value will automatically apply physics to an object. What it does to stop your object when it collides with the object with the assigned `collisionBitMask`
- `contactTestBitMask` will **notify** you of the collision/contact. Adopt the `SKPhysicsContactDelegate` to your scene class, set the `contactDelegate` and implement the delegate methods to customise what happens when there's contact between two physics bodies.
- The preferred order in `SpriteKit` is to 
- This is an example showing how to make the scene's frame a border so other physics bodies won't go beyond it.
``` swift
let borderBody = SKPhysicsBody.init(edgeLoopFrom: self.frame)
self.physicsBody = borderBody
self.physicsBody?.categoryBitMask = Collision.Block
self.physicsBody?.collisionBitMask = Collision.Player
```
- `self.playerSprite?.physicsBody?.applyImpulse(CGVector.init(dx: 0, dy: -15))` applying impulse basically bounces off your object from say, a wall. Use the `contactTestBitMask` for this. `collisionBitMask` does the job but only once.
