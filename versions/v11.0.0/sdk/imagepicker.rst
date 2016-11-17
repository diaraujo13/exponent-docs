ImagePicker
===========

Provides access to the system's UI for selecting images from the phone's photo
library or taking a photo with the camera.

.. function:: Exponent.ImagePicker.launchImageLibraryAsync(options)

   Display the system UI for choosing an image from the phone's photo library.

   :param object options:
      A map of options:

      * **allowsEditing** (*boolean*) -- Whether to show a UI to edit the image
        after it is picked. On Android the user can crop and rotate the image
        and on iOS simply crop it. Defaults to ``false``.

      * **aspect** (*array*) -- An array with two entries ``[x, y]`` specifying the
        aspect ratio to maintain if the user is allowed to edit the image (by
        passing ``allowsEditing: true``). This is only applicable
        on Android, since on iOS the crop rectangle is always a square.

   :returns:
      If the user cancelled the image picking, returns ``{ cancelled: true }``.

      Otherwise, returns ``{ cancelled: false, uri, width, height }`` where
      ``uri`` is a URI to the local image file (useable in a react-native
      ``Image`` tag) and ``width, height`` specify the dimensions of the image.

.. function:: Exponent.ImagePicker.launchCameraAsync(options)

   Display the system UI for taking a photo with the camera.

   :param object options:
      A map of options:

      * **allowsEditing** (*boolean*) -- Whether to show a UI to edit the image
        after it is picked. On Android the user can crop and rotate the image
        and on iOS simply crop it. Defaults to ``false``.

      * **aspect** (*array*) -- An array with two entries ``[x, y]`` specifying the
        aspect ratio to maintain if the user is allowed to edit the image (by
        passing ``allowsEditing: true``). This is only applicable
        on Android, since on iOS the crop rectangle is always a square.

   :returns:
      If the user cancelled taking a photo, returns ``{ cancelled: true }``.

      Otherwise, returns ``{ cancelled: false, uri, width, height }`` where
      ``uri`` is a URI to the local image file (useable in a React Native
      ``Image`` tag) and ``width, height`` specify the dimensions of the image.


Example

::
import React from 'react';
import {
  Image,
  Linking,
  Platform,
  ScrollView,
  StyleSheet,
  Text,
  TouchableOpacity,
  View,
} from 'react-native';
import Exponent from 'exponent';

export default class HomeScreen extends React.Component {
  render() {
    return (
      <View style={styles.container}>
            <TouchableOpacity onPress={ ()=> this.openImage() }>
                  <View>
                        <Text>Carregar Imagem</Text>
                  </View>
            </TouchableOpacity>
      </View>
    );
  }

  openImage(){
        Exponent.ImagePicker.launchImageLibraryAsync(
             {
                   allowsEditing:true,
                   aspect: [4,3]
             }
      ).then(
         (data)=>{
            console.log(data);
      }
      );
 }
}  


Output:
``{"cancelled":false,"height":1611,"width":2148,"uri":"file:///data/user/0/host.exp.exponent/cache/cropped1814158652.jpg"}``
