## AnchorKit

AnchorKit is a Auto Layout easy on both iOS.

## Contents

- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [License](#license)

## Requirements

- iOS 11.0+
- Xcode 10.0+
- Swift 4.0+

## Installation

### Swift Package Manager
> Xcode 10+ is required to build AnchorKit using Swift Package Manager.

1. In Xcode, with your app project open, navigate to File > Add Packages.
2. When prompted, add the AnchorKit Apple platforms SDK repository:

```swift
  https://github.com/habiboff/AnchorKit.git
```

## Usage

#### Constraint AutoLayout

```swift
import AnchorKit

class MainViewController: UIViewController {

    private let redView: UIView = {
       let view = UIView()
        view.backgroundColor = .red
        return view
    }()

    private let blueView: UIView = {
       let view = UIView()
        view.backgroundColor = .blue
        return view
    }()

    override func viewDidLoad() {
        super.viewDidLoad()

        view.anchor(view: redView) { kit in
            kit.leading(16)
            kit.top(16, safe: true)
            kit.width(100)
            kit.height(100)
        }
        
        view.anchor(view: blueView) { kit in
            kit.leading(16)
            kit.top(redView.bottomAnchor, 10)
            kit.trailing(16)
            kit.height(150)
        }
    }
}
```
#### Constraint UITableView and configure example

```swift
import AnchorKit

class ViewController: UIViewController {
    
    private var names: [String] = ["Apple", "Amazon", "Tesla", "Github"]
    
    lazy var tableView: UITableView = {
        return .init(cell: UITableViewCell.self, delegate: self, dataSource: self)
    }()
    
    override func viewDidLoad() {
        super.viewDidLoad()
        view.backgroundColor = .white
        
        view.anchorFill(view: tableView, safe: true)
    }
}

extension ViewController: UITableViewDelegate, UITableViewDataSource {
    
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return names.count
    }
    
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        return tableView.reuseable(cell: UITableViewCell.self, indexPath: indexPath) { cell in
            cell.textLabel?.text = self.names[indexPath.row]
        }
    }
    
    func tableView(_ tableView: UITableView, heightForRowAt indexPath: IndexPath) -> CGFloat {
        return 60
    }
}
```

##### StackView • VStack & HStack (Method 1)

```swift
import AnchorKit

class MainViewController: UIViewController {

    private let redView: UIView = {
       let view = UIView()
        view.backgroundColor = .red
        view.heightAnchor.constraint(equalToConstant: 50).isActive = true
        return view
    }()

    private let blueView: UIView = {
       let view = UIView()
        view.backgroundColor = .blue
        view.heightAnchor.constraint(equalToConstant: 50).isActive = true
        return view
    }()

    override func viewDidLoad() {
        super.viewDidLoad()
        let viewHolder = VStack(views: redView, blueView, spacing: 10, distribution: .fillEqually)
        view.anchor(view: viewHolder) { kit in
            kit.leading(24)
            kit.top(20, safe: true)
            kit.trailing(24)
        }
    }
}
```

##### StackView • VStack & HStack (Method 2)

```swift
import AnchorKit

class MainViewController: UIViewController {
    
    private let redView: UIView = {
       let view = UIView()
        view.backgroundColor = .red
        return view
    }()

    private let blueView: UIView = {
       let view = UIView()
        view.backgroundColor = .blue
        return view
    }()

    override func viewDidLoad() {
        super.viewDidLoad()
        view.backgroundColor = .white
        
        let viewHolder = VStack(views: redView.withHeight(50), blueView.withHeight(50), spacing: 10, distribution: .fillEqually)
        view.anchor(view: viewHolder) { kit in
            kit.leading(24)
            kit.top(20, safe: true)
            kit.trailing(24)
        }
    }
}
```

##### StackView • VStack & HStack (Method 3)

```swift
import AnchorKit

class MainViewController: UIViewController {
    
    private let redView: UIView = {
       let view = UIView()
        view.backgroundColor = .red
        return view
    }()

    private let blueView: UIView = {
       let view = UIView()
        view.backgroundColor = .blue
        return view
    }()

    override func viewDidLoad() {
        super.viewDidLoad()
        view.backgroundColor = .white
        
        let viewHolder = VStack(views: redView, blueView, spacing: 10, distribution: .fillEqually)
        view.anchor(view: viewHolder) { kit in
            kit.leading(24)
            kit.top(20, safe: true)
            kit.trailing(24)
            kit.height(100)
        }
    }
}
```
<img src="https://github.com/habiboff/AnchorKit/blob/master/SatckView3.png" alt="" />

##### StackView • VStack & HStack (Method 4)

```swift
import AnchorKit

class MainViewController: UIViewController {
    
    private let redView: UIView = {
       let view = UIView()
        view.backgroundColor = .red
        return view
    }()

    private let blueView: UIView = {
       let view = UIView()
        view.backgroundColor = .blue
        return view
    }()
    
    private let purpleView: UIView = {
       let view = UIView()
        view.backgroundColor = .purple
        return view
    }()

    override func viewDidLoad() {
        super.viewDidLoad()
        view.backgroundColor = .white
        
        let verticalViews = VStack(views: redView, blueView, spacing: 5, distribution: .fillEqually)
        let horizontalView = HStack(views: purpleView, verticalViews, spacing: 5, distribution: .fillEqually)
        
        view.anchor(view: horizontalView) { kit in
            kit.leading(24)
            kit.top(20, safe: true)
            kit.trailing(24)
            kit.height(150)
        }
    }
}
```

##### StackView • VStack & HStack (Method 5)

```swift
import AnchorKit

class MainViewController: UIViewController {
    
    private let redView: UIView = {
       let view = UIView()
        view.backgroundColor = .red
        return view
    }()

    private let blueView: UIView = {
       let view = UIView()
        view.backgroundColor = .blue
        return view
    }()
    
    private let purpleView: UIView = {
       let view = UIView()
        view.backgroundColor = .purple
        return view
    }()

    override func viewDidLoad() {
        super.viewDidLoad()
        view.backgroundColor = .white
        
        let verticalViews = VStack(views: redView, blueView, spacing: 5, distribution: .fillEqually)
        let leftView = HStack(views: purpleView).padRight(30)
        let horizontalView = HStack(views: leftView, verticalViews, spacing: 5, distribution: .fillEqually)
        
        view.anchor(view: horizontalView) { kit in
            kit.leading(24)
            kit.top(20, safe: true)
            kit.trailing(24)
            kit.height(150)
        }
    }
}
```

## License

AnchorKit is released under the MIT license.
