# Liskov Substitution

> Derived classes must be substitutable for their base classes.

> Any implementation of an abstraction should be suitable anywhere the abstraction is accepted.

## Good practices
- Signature must match
- Preconditions can't be greater
- Post conditions at least equal to
- Exception types must match

## Code example - video player
```php
<?php
class VideoPlayer {
	public function play()
	{
		// play the video
	}
}

class AviVideoPlayer extends VideoPlayer {
	public function play($file)
	{
		// Violates the Liskov substitution principle
		if (pathinfo($file, PATHINFO_EXTENSION) !== 'avi')
		{
			throw new Exception;
		}
	}
}
?>
```

## Code example - video player
```php
<?php
interface LessonRepositoryInterface {
	// We can't enforce the return value of this function
	public function getAll();
}

class FileLessonRepository implements LessonRepositoryInterface {
	public function getAll()
	{
		// Use the filesystem
		return [];
	}
}

class DbLessonRepository implements LessonRepositoryInterface {
	public function getAll()
	{
		// Violates the Liskov substitution principle
		// It returns an Eloquent collection instead of an array
		return Lesson::all();
	}
}

function foo(LessonRepositoryInterface $lesson)
{
	$lessons = $lesson->getAll();
	// We may be force to test the type of $lessons..
}
?>
```