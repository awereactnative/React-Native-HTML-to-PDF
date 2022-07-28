# React-Native-HTML-to-PDF
Convert html strings to PDF documents using React Native.

# Demo 

<img width="362" alt="htmlToPdf" src="https://user-images.githubusercontent.com/86215353/181406184-41605529-cb16-4f00-bb42-5c876d75e181.png">


## Installation
Run below commands

```
npm install react-native-html-to-pdf --save

```
### Option 1: Automatic
```
react-native link
```

### Option 2: Manual
#### iOS
2. Open your project in XCode, right click on Libraries and select Add Files to "Your Project Name.
3. Add libRNHTMLtoPDF.a to Build Phases -> Link Binary With Libraries (Screenshot).

#### Android
- Edit android/settings.gradle to included.

```
include ':react-native-html-to-pdf'
project(':react-native-html-to-pdf').projectDir = new File(rootProject.projectDir,'../node_modules/react-native-html-to-pdf/android')
```

- Edit android/app/build.gradle file to include.

```
dependencies {
  compile project(':react-native-html-to-pdf')
}
```

- Edit MainApplication.java to include.

```
// import the package
import com.christopherdro.htmltopdf.RNHTMLtoPDFPackage;

// include package
new MainReactPackage(),
new RNHTMLtoPDFPackage()
```

- Add the following WRITE_EXTERNAL_STORAGE permission to AndroidManifest.xml.

```
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```

Also starting from Android M, users need to be prompted for permission dynamically. Follow [this](https://facebook.github.io/react-native/docs/permissionsandroid) link for more details on how to do that.

## Usage
```javascript
import React, { Component } from 'react';

import {
  Text,
  TouchableHighlight,
  View,
} from 'react-native';

import RNHTMLtoPDF from 'react-native-html-to-pdf';

export default class Example extends Component {
  async createPDF() {
    let options = {
      html: '<h1>PDF TEST</h1>',
      fileName: 'test',
      directory: 'Documents',
    };

    let file = await RNHTMLtoPDF.convert(options)
    // console.log(file.filePath);
    alert(file.filePath);
  }

  render() {
    return(
      <View>
        <TouchableHighlight onPress={this.createPDF}>
          <Text>Create PDF</Text>
        </TouchableHighlight>
      </View>
    )
  }
}
```
## Options

| Param     | Type     | Default     | Note     |
| ---------- | ---------- | ---------- | ---------- |
| __html__       | string       |        | HTML string to be converted       |
| __base64__       | boolean       | false       | return base64 string of pdf file (not recommended) |
| __directory__       | string       | default cache directory | Directory where the file will be created (__Documents__ folder in example above). Please note, on iOS __Documents__ is the only custom value that is accepted. |
| __height__       | number       | 792       | Set document height (points)       |
| __width__       | number       | 612       | Set document width (points)       |

### iOS Only
| Param     | Type     | Default     | Note     |
| ---------- | ---------- | ---------- | ---------- |
| __paddingLeft__       | number       | 10       | 	Outer left padding (points)|
| __paddingRight__       | number       | 10       |	Outer right padding (points)|
| __paddingTop__       | number       | 10 | Outer top padding (points) |
| __paddingBottom__       | number       | 10       | Outer bottom padding (points)|
| __padding__       | number       | 10       | 	Outer padding for any side (points), overrides any padding listed before |
| __bgColor__       | string       | #F6F5F0       | 	Background color in Hexadecimal   |

### Android Only
| Param     | Type     | Default     | Note     |
| ---------- | ---------- | ---------- | ---------- |
| __fonts__       | Array       |       | 	Allow custom fonts __['/fonts/TimesNewRoman.ttf', '/fonts/Verdana.ttf']__|
