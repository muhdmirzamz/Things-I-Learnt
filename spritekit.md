## SpriteKit

- Just giving ```collisionBitMask``` a value will automatically apply physics to an object. Default behaviour is to bounce off collided objects.
- ```contactTestBitMask``` will **notify** you of the collision/contact. Adopt the ```SKPhysicsContactDelegate``` to your scene class, set the ```contactDelegate``` and implement the delegate methods to customise what happens when there's contact between two physics bodies.
