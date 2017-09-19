## SpriteKit

- The way ```SpriteKit``` works is that it has an ```SKView``` holding an ```SKScene```. So if you want to get the width or anything, it's not ```self.view.frame.size.width```. Instead, it's ```self.size.width```. If you refer to ```self.view```, it refers to the ```SKView```
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
- ```monsterSprite.physicsBody?.isDynamic = true``` Imagine a person hits you on the shoulder while both of you are walking towards one another. You would be taken aback into the direction of the hit right? That's what this code does. Basic physics right there. Setting this to false on both category bit masks will result in each sprite of each bitmask to just pass through each other without collision.
- If you want to detect multiple contacts of ```SKPhysicsBody```, use the code from [here](https://stackoverflow.com/a/26331003). Basically check the relation of the bitmasks, which sprite has the lower bitmask. From there, verify that it is the real bitmask you are looking for.
- When checking for bitmasks, the current way may seem inefficient because you are checking which sprite has the lower bitmasks first, then assigning. Sure, you can assign straight away, but that results in some highly duplicated code. And you don't want that. It results in duplicated code because you have 2 physics bodies in contact and ```SpriteKit``` cannot which sprite is which. Hence the first part is sort of a trial and error to find out.
``` swift
if contact.bodyA.categoryBitMask < contact.bodyB.categoryBitMask {
	monsterBody = contact.bodyA
	projectileBody = contact.bodyB
} else {
	monsterBody = contact.bodyB
	projectileBody = contact.bodyA
}

if monsterBody.categoryBitMask == Collision().Monster && projectileBody.categoryBitMask == Collision().Projectile {

}
```
- This is how you make a sprite follow a path
``` swift
let path = CGMutablePath()
path.move(to: CGPoint.init(x: 50, y: 50))
path.addLine(to: CGPoint.init(x: 200, y: 50))
path.addLine(to: CGPoint.init(x: 200, y: 100))
path.addLine(to: CGPoint.init(x: 50, y: 100))

let moveAction = SKAction.follow(path, asOffset: false, orientToPath: true, duration: 2)

let forever = SKAction.repeatForever(moveAction)
monsterSprite.run(forever)
```
- Notes about sprites following a path, 
``` swift
let moveAction = SKAction.follow(path, asOffset: false, orientToPath: true, duration: 2)
```
`asOffset: true` means if your sprite is at (50, 50) and you want it to `path.move(to: CGPoint.init(x: 50, y: 50))`, it adds 50 to the sprite's current position. So, set `offset` to false.

`orientToPath: true` means your sprite faces the direction it is going to.
``` swift
let moveAction = SKAction.follow(path, asOffset: false, orientToPath: true, duration: 2)
let moveAction2 = SKAction.follow(path, duration: 2)
```
Top method provides options for `asOffset` but method below defaults to true. Got to pay attention on this one.
- Read (this)[https://stackoverflow.com/questions/21505660/physics-bodies-not-responding-to-bitmask-settings#comment60916704_21508132] regarding testing for sprite contact or collision 


