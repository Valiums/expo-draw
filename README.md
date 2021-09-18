# Expo Draw (Valiums's fork)

Expo draw tool using react-native-svg. (Forked from [rn-draw](https://github.com/jayeszee/rn-draw))

[![rn-draw.gif](https://s1.gifyu.com/images/rn-draw.gif)](https://gifyu.com/image/pLIr)

`with color support`
[![image0.png](https://cdn.discordapp.com/attachments/688484592348561446/888727147072589894/image0.png)](https://cdn.discordapp.com/attachments/688484592348561446/888727147072589894/image0.png)

# Installation

First install [react-native-svg](https://github.com/react-native-community/react-native-svg) `expo install react-native-svg`

Then install expo-draw with `npm install --save git+https://github.com/Valiums/expo-draw`

# How to use

```
import ExpoDraw from 'expo-draw'

<ExpoDraw
  strokes={[]}
  containerStyle={{backgroundColor: 'rgba(0,0,0,0.01)'}}
  rewind={(undo) => {this._undo = undo}}
  clear={(clear) => {this._clear = clear}}
  color={'#000000'} // you can change the color here. Each stroke will save its current color.
  strokeWidth={4}
  enabled={true}
  onChangeStrokes={(strokes) => console.log(strokes)}
/>

### Props
**strokes** [Array] - set with some initial data. (defaults to [])

**containerStyle** [Object] - style for the container of the draw component.

**color** [String] - string representation of pen color (defaults to '#000000')

**strokeWidth** [Number] - width of pen strokes (defaults to 4)

**rewind** [Func] - a function for passing the draw component's undo functionality

**clear** [Func] - a function for passing the draw component's clear functionality

**onChangeStrokes** [Func] - callback that is called when the draw changes.

**enabled** [Boolean] - set if user can edit it. If false it disable also all touch event, so you can use it easly on GestureView like ScrollView.
```

# Tips when implementing

You can save a screenshot of your canvas using `takeSnapshotAsync`, the method from expo, like so:

```
import { captureRef as takeSnapshotAsync } from 'react-native-view-shot';

mySaveFx = async () => {
	const signatureResult = await takeSnapshotAsync(this.refOfExpoDrawElement, {
		result: 'tmpfile',
		quality: 0.5,
		format: 'png',
	});

  //The output will be a local tmpfile (uri)[String], with the current lines that were drawn. Therefore, you can save it or so! ;)
  console.log(signatureResult);
}

```

You can also save strokes array as json, for example, on firebase. In order to support all displays i recommend to use fixed dimensions:

```

  state = {
    strokes: []
  }

  saveOnFirebase = () => {
    firebase.firestore().collection('signature').doc().set({strokes})
  }

  render() {
    return(
      <View>
        <ExpoDraw
          strokes={[]}
          containerStyle={{backgroundColor: 'rgba(0,0,0,0.01)', height: 300, width: 500}}
          rewind={(undo) => {this._undo = undo}}
          clear={(clear) => {this._clear = clear}}
          color={'#000000'}
          strokeWidth={4}
          enabled={true}
          onChangeStrokes={(strokes) => this.setState({strokes})}
        />
        <Button onPress={saveOnFirebase} title={"Save my signature"}/>
      </View>
    )
  }


```

# Context on why I forked

This is actually a fork of a fork.
I needed to add support for colors.

I created this fork because I don't think their repos are still being maintained.
If you ever need color supports, use my fork at your own risk.
I'll probably not maintain this.

All the heavy work was actually done by
[rn-draw](https://github.com/jayeszee/rn-draw)
and
[expo-draw](https://github.com/MarangoniEduardo/expo-draw)

Credits goes to them!
