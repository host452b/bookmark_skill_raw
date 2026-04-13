**Attention**
Topic was automatically imported from the old Question2Answer platform.

**Asked By**
NaughtyGnosiophile

I have a game that has many enemies, implemented with KinematicBody2D, that move around and bump into each other.

I move them in `_physics_process()` like this:
```
func _physics_process(delta):
	var tree = get_tree()
	tree.call_group("creeps", "calc_velocity")
	tree.call_group("creeps", "move_position", delta)

```

This is the `move_position()` function in each enemy:
```
func move_position(delta):	
	var collision = _host.move_and_collide(velocity * delta)	
	if _rotation_on:
		_host.rotation = velocity.angle()
	
	if collision and !_host.handle_collision(collision):
		velocity = velocity.slide(collision.normal)
		_host.move_and_slide(velocity)

```

I can see from the profiler the spikes happen every time I spawn a new group of enemies.  There may be 100-200 enemies on the screen at the same time.  I would like to be able to spawn up to 500 enemies.

                    [
            
          ](https://dl.dropboxusercontent.com/s/ieydckz0apzqp9j/frame_time_profile.png?dl=0)

The game and controls get really laggy.

Does Frame Time 1000% mean it’s taking 10 times as long to process a frame than it’s supposed to?

I can also see that the `move_position`function is taking a lot of time.

                    [
            
          ](https://dl.dropboxusercontent.com/s/gzno61edtqv8eum/move_position_profile.png?dl=0)

So how can I fix this?

Is KinematicBody2D fundamentally too heavy?  Is it practical to implement with Area2D?  Would that even help?

Or maybe my enemy node structure is too complex?

                    [
            
          ](https://dl.dropboxusercontent.com/s/50nvc0mkfqr9881/unit_structure.png?dl=0)

I know there are lots of games with many enemies in them so I know it can be done, but not sure if I’m doing this the proper way.  Any help appreciated.

`tree.call_group("creeps", "calc_velocity")` → is this piece of code in the script of every creep? I hope not, because if you have 500 creeps that means it will run `calc_velocity` 250,000 times for no reason.

Also your enemy structure might be too complex for 500 creeps, it looks like a single creep already does quite a lot of stuff, but I can’t tell if it’s actually the slow part, for now the current bottleneck are the two functions you call with `call_group`. Perhaps also look in `_host.handle_collision` and collision signal handlers?

Zylann | 2018-10-19 17:20

Oops.  Didn’t get a notification for this for some reason…

I have a “game controller” that calls `tree.call_group("creeps", "calc_velocity")` in every physics cycle.  So `calc_velocity` is only called once per creep every physics cycle.

This is the default implementation of my `handle_collision`:
```
func handle_collision(collision):
	if is_melee_behaviour:
		var collider = collision.collider
		if collider.is_in_group("bunker") or collider.is_in_group("shooter"):
			attack(collider)
			return true
			
	return false

```

I don’t feel like it’s too heavy.

But I think you might be right that each unit based on a KinematicBody2D is rather heavy.  If so, what would be an alternate implementation?

Something like keeping track of all the creep positions in some kind of structure and doing a manual draw for each of them, forgoing use of the physics engine completely?  But then wouldn’t I need to keep track of collisions myself, in essence then re-implementing the physics engine?  This would be a fairly significant rewrite and I’m not sure if this would solve it or be practical.

NaughtyGnosiophile | 2018-11-24 15:56

I have the same issue. In my case with rigidbodies, once I add 100 of them and control them as per the documentation in _integrateforces the game starts to choke . I have tried converting them to KinematicBody2Ds but the performance is still not going to work out. I’ve been stripping out as much of the logic as possibly on the enemy scene but to no avail as of yet.

I want to continue with Godot but I’ve read other reports around these performance problems and it’s beginning to concern me.

This post may be useful, ref: shower of bullets demo and custom physics server

[Reddit - Dive into anything](https://www.reddit.com/r/godot/comments/8poaky/comment/e0d0zef)

christh | 2018-12-21 02:03