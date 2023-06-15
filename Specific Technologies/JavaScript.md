#Switch-Statement

Using a switch statement can be useful as an alternative to if/else when we have multiple options (e.g. rolling dice).
```javascript
function playSoundEffect(effect) {
	switch (effect) {
		case "rain":
			if (isRainPlaying) {
				rainAudio.pause();
				rainAudio.currentTime = 0;
				isRainPlaying = false;
			} else {
			rainAudio.play();
			isRainPlaying = true;
		}
		break;
		case "fireplace":
			if (isFireplacePlaying) {
				fireplaceAudio.pause();
				fireplaceAudio.currentTime = 0;
				isFireplacePlaying = false;
				} else {
				fireplaceAudio.play();
				isFireplacePlaying = true;
			}
			break;
			}
```

