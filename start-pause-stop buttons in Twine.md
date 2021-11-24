https://twinery.org/forum/discussion/1876/how-to-make-a-pause-and-mute-button-in-menuoptions


https://twinery.org/forum/discussion/5048/audio-turn-off-on-option-in-sugarcube-2-where-to-upload

The answer is well over a year old. While it does still work, I'd write it differently today—post-v2.8.0, where the <<masteraudio>> macro (http://www.motoslave.net/sugarcube/2/docs/macros.html#macros-masteraudio) and << createplaylist >> <>macro (http://www.motoslave.net/sugarcube/2/docs/macros.html#macros-createplaylist) exist.  
  
Story JavaScript:

var audioEnabledHandler = function () {
	if (!settings.audioEnabled) { // is false
		/*
			Stops all audio currently playing, via <<audio>> or <<playlist>>,
			when the setting is disabled.
		*/
		new Wikifier(null, "<<masteraudio stop>>");
	}
};
Setting.addToggle("audioEnabled", {
	label    : "Enable audio within the story?",
	default  : true,
	onInit   : audioEnabledHandler,
	onChange : audioEnabledHandler
});

And checking the setting wherever you wish to play audio. For example:

/* To play a single track. */
<<if settings.audioEnabled>><<audio "someTrack" play>><</if>>

/* To play a playlist. */
<<if settings.audioEnabled>><<playlist "somePlaylist" play>><</if>>