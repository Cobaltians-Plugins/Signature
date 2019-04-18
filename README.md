# Signature Plugin

Signature plugin allows to draw a signature and save it.

### How to use

* import the plugin to your project as explained [here](https://github.com/cobaltians/cobalt/wiki/Plugins-usage)
* Add the cobalt.signature.js to your web JS folder
* Add an html link to the cobalt.signature.js plugin script after the cobalt link in the HEAD tag
* For Android : add those lines to your fragment's onActivityResult:

```
@Override
public void onActivityResult(int requestCode, int resultCode, Intent data)
{
	// Forward result for Signature
	Signature signature = (Signature) Signature.getInstance(new CobaltPluginWebContainer(getActivity(),	this));
	signature.onActivityResult(requestCode, resultCode, data);

	super.onActivityResult(requestCode, resultCode, data);
}
```

## signature

Use the `cobalt.signature.sign` shortcut like this


```
cobalt.signature.sign({
    size: 500
  }, function(data){
    cobalt.log('status', data.status, data);
});
```

* params : `{ size: 500 }` or `{}`. size is optional and default to 800.

The drawing screen opens empty, with instructions on bottom of the screen.

If User start drawing on empty screen : Instructions are hidden, and `Clear` button appears.

Pressing `Clear` button : Clear the current drawing, `Clear` button is hidden, and Instructions are displayed.

Pressing `Save` button : Save current drawing in local, and sends a callback to web with id and base64 String of the saved signature.

```
{ 
    id: 'yourPictureId', 
    picture: 'theBase64StringOfThePicture',
}
```

If drawing screen is empty, callback sends an empty data object.

Pressing `Back` button closes the drawing screen snd does not send anything to the web.
