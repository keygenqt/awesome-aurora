# Toast в Aurora OS

Всем знакомый "Toast" вы не найдете в Аврора ОС.
Но не печальтесь я расскажу вам как сделать нотификацию очень схожую с привычным всем Toast-ом.
В Аврора ОС компонент похожий на "Toast" называется Notices.
Вызов его будет выглядеть следующим образом:

```qml
Notices.show(
    "Text toast",
    Notice.Short,
    Notice.Bottom,
    0,
    -Theme.horizontalPageMargin)
```

### Параметры

| Name                 | Type    | Default        | Values                           |
|----------------------|---------|----------------|----------------------------------|
| `text`               | QString | -              | String                           |
| `duration`           | Notice  | Notice::Long   | Short, Long                      |
| `anchor`             | Notice  | Notice::Bottom | Center, Left, Right, Top, Bottom |
| `horizontalOffset`   | qreal   | 0              | Number                           |
| `verticalOffset`     | qreal   | 0              | Number                           |

### Пример

```qml
import QtQuick 2.0
import Sailfish.Silica 1.0

Page {
    objectName: "mainPage"
    allowedOrientations: Orientation.All

    PageHeader {
        objectName: "pageHeader"
        title: qsTr("Application Template")
        extraContent.children: [
            IconButton {
                objectName: "aboutButton"
                icon.source: "image://theme/icon-m-about"
                anchors.verticalCenter: parent.verticalCenter

                onClicked: pageStack.push(Qt.resolvedUrl("AboutPage.qml"))
            }
        ]
    }

    Button {
        anchors.centerIn: parent
        text: qsTr("Вызвать Toast")
        onClicked: Notices.show(
                      "Моя очень длинная Toast нотификация для Авроры ОС",
                      Notice.Short,
                      Notice.Bottom,
                      0,
                      -Theme.horizontalPageMargin)
    }
}
```

### Preview

![my_gif.gif](data%2Fmy_gif.gif)
