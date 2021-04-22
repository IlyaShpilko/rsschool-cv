1. Name: Shpilko Ilya

2. Contact Information:
Address: Saratov region, city of Engels
Phone: 8 (905) 383-38-75
@email: shpilkoilya@icloud.com
github: https://github.com/IlyaShpilko

3. Resume (your goal, wishes, reveal what is important to you, what you want and why.

I dream of developing and learning something new. All my life I have always learned something and this knowledge is served to me both in everyday life and in everything I touch. In programming, too, you constantly learn something, constantly think over some ideas. Therefore, I chose this direction and want to become a programmer.

4. Skills (e.g. programming languages, frameworks, methodologies, version control, tools, etc.)

- Xcode
- Swift
- Objective-C
- Foundation
- UIKit
- CoreData
- GCD
- Git

5. Code Examples (LAST)

'''SWIFT

    import UIKit
    import CoreData

    class HomeTableViewController: UITableViewController, UITextFieldDelegate {
    
    struct Task {
        var text: String
        var id: Int
    }
    
    var alertController: UIAlertController? = nil
    var alertAction: UIAlertAction? = nil
    
    var array = [AddText]()
    
    let context = (UIApplication.shared.delegate as! AppDelegate).persistentContainer.viewContext

    override func viewDidLoad() {
        super.viewDidLoad()
        
        navigationItem.rightBarButtonItem = UIBarButtonItem(barButtonSystemItem: .add, target: self, action: #selector(buttonTapped))
        
        tableView.register(UINib(nibName: "HomeTableViewCell", bundle: nil), forCellReuseIdentifier: "HomeTableViewCell")
        fetchText()
    }
    
    @objc func buttonTapped() {
        alertController = UIAlertController(title: "Add new element in table", message: "Enter text", preferredStyle: .alert)
        
        alertController?.addTextField() { (text) in
            
            text.addTarget(self, action: #selector(self.textFieldDidChangeSelection(_:)), for: .editingChanged)
            
        }
        
        alertAction = UIAlertAction(title: "Add", style: .default, handler: { (action) in
            
            let textField = self.alertController?.textFields![0]
            
            let addNewElement = AddText(context: self.context)
            addNewElement.writeText = textField?.text
            addNewElement.idNumber = random()
            self.saveContent()
        })
        
        alertController?.addAction(alertAction!)
        present(alertController!, animated: true) {
            self.alertAction?.isEnabled = false
        }
    }
    
    //MARK: -TextFieldDelegate
    func textFieldDidChangeSelection(_ textField: UITextField) {
        guard let checkText = textField.text?.count else { return }
        
        if checkText >= 3 {
            self.alertAction?.isEnabled = true
        } else {
            self.alertAction?.isEnabled = false
        }
    }
    
    // MARK: - Table view data source
    override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return array.count
    }
    
    override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "HomeTableViewCell", for: indexPath)
        
        let textView = self.array[indexPath.row]
        
        cell.textLabel?.text = "(\(textView.idNumber)) \(textView.writeText ?? "")"
        
        return cell
    }
    
    // Override to support editing the table view.
    override func tableView(_ tableView: UITableView, commit editingStyle: UITableViewCell.EditingStyle, forRowAt indexPath: IndexPath) {
        if editingStyle == .delete {
            
            let textRemove = array[indexPath.row]
            self.context.delete(textRemove)
            
            saveContent()
        }
    }
    
    override func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        let writeText = array[indexPath.row]
        
        alertController = UIAlertController(title: "Edit text", message: nil, preferredStyle: .alert)
        alertController?.addTextField() { (text) in
            
            text.addTarget(self, action: #selector(self.textFieldDidChangeSelection(_:)), for: .editingChanged)
            
        }
        
        let editText = self.alertController?.textFields![0]
        editText?.text = writeText.writeText
        
        alertAction = UIAlertAction(title: "Edit", style: .default, handler: { (action) in
            let editText = self.alertController?.textFields![0]
            writeText.writeText = editText?.text
            
            self.saveContent()
        })
        
        alertController?.addAction(alertAction!)
        present(alertController!, animated: true) {
            self.alertAction?.isEnabled = true
        }
    }
    
    //MARK: - Core data
    func fetchText() {
        do {
            self.array = try context.fetch(AddText.fetchRequest())
            DispatchQueue.main.async {
                self.tableView.reloadData()
            }
        } catch let error as NSError {
            print("error: \(error), userInfo: \(error.userInfo)")
        }
    }
    
    func saveContent() {
        do {
            try self.context.save()
        } catch let error as NSError {
            print("error: \(error), userInfo: \(error.userInfo)")
        }
            self.fetchText()
        }
    }

    func random() -> Int64{
        return Int64(Int.random(in: 0...100_000))
    }
    '''

6. Experience (for a junior developer, this means all kinds of experience: coding tests, projects from courses,
freelance projects - wherever they had the opportunity to demonstrate their skills.
It would also be great if you add links to the source code)
Learning experience:
- Crimea Digital Group - MOBILE IOS

7. Training (including courses, seminars, lectures, online training)
I was self-taught. Learning experience:
- Crimean digital group - MOBILE IOS


8. The last English grade was A2
