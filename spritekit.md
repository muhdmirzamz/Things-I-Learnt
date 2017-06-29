## SpriteKit

- Just giving `collisionBitMask` a value will automatically apply physics to an object. What it does to stop your object when it collides with the object with the assigned `collisionBitMask`
- `contactTestBitMask` will **notify** you of the collision/contact. Adopt the `SKPhysicsContactDelegate` to your scene class, set the `contactDelegate` and implement the delegate methods to customise what happens when there's contact between two physics bodies.
- The preferred order in `SpriteKit` is to 
  - init the object, set the position and add it as a child to the scene
  - Apply physics to it
  - Apply action/motion to it
- This is an example showing how to make the scene's frame a border so other physics bodies won't go beyond it.
``` swift
let borderBody = SKPhysicsBody.init(edgeLoopFrom: self.frame)
self.physicsBody = borderBody
self.physicsBody?.categoryBitMask = Collision.Block
self.physicsBody?.collisionBitMask = Collision.Player
```
- `self.playerSprite?.physicsBody?.applyImpulse(CGVector.init(dx: 0, dy: -15))` basically bounces your object off from say, a wall. Use the `contactTestBitMask` for this. `collisionBitMask` does the job but only once.
- The piece of code below spawns monsters in a game infinitely. Without ```SKAction.wait(forDuration: 1.0)```, the amount of memory used will be huge. From the simulator, nothing will display. My guess is it uses so much memory it starts to lag.
``` swift
run(SKAction.repeatForever(SKAction.sequence([SKAction.run {
			self.addMonster()
			}, SKAction.wait(forDuration: 1.0)])))
```
