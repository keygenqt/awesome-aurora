Пример с ViewModel (Qt/Qml)
===================

#### ViewModel

```cpp
class ViewModel : public QObject
{
    Q_OBJECT
    Q_PROPERTY(int counter READ counter NOTIFY counterChanged)
public:
    ViewModel() = default;
    ~ViewModel() = default;

    int counter() const { return m_counter; }
    Q_SIGNAL void counterChanged();

public slots:
    void incrementCounter() {
        m_counter++;
        emit counterChanged();
    }

private:
    int m_counter = 0;
};
```

#### QML

```cpp
import QtQuick 2.0

Item {
    property alias counter: label.text
    property ViewModel viewModel: ViewModel {}

    Column {
        Label {
            id: label
            text: viewModel.counter
        }
        Button {
            text: "Increment"
            onClicked: viewModel.incrementCounter()
        }
    }
}
```

#### Application

```cpp
import QtQuick 2.0

ApplicationWindow {
    visible: true
    width: 640
    height: 480

    Component.onCompleted: viewModel.counterChanged.connect(function(){console.log("Counter Changed")})

    View {
        viewModel: ViewModel {}
        anchors.fill: parent
    }
}
```