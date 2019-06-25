# ioSwift

### Novo Projeto
Organization Identifier: com.[nome da empresa]


#### GIT

git init: inicia um repositório local

git add <NomeDoArquivo> ou git add . (para todos os arquivos)
passa os arquivos para a ‘staging área’ - importante para definir quais arquivos do projeto o git vai ignorar

git rm —cached -r . (desfaz o git add .)

git commit -m “Mensagem”
passa os arquivos para o repositório local

git status: mostra os arquivos ignorados ou os novos incluídos

git log: mostra os registros dos commits

git checkout <NomeDoArquivo> retorna o arquivo para a situação do último comia

Repositório Remoto
1) criar repo no GitHub.com
2) git remote add origin <https do repositório>
3) git push -u origin master

origin: nome do remoto
master: nome do branch

.gitignore
arquivo com a lista de arquivos a ser ignorados no commit (ex: api keys, secrets, arquivos desnecessários…)

touch .gitignore : o comando touch cria o arquivo com esse nome
open .gitignore: abre
no GitHub existe um repositório chamado github/gitignore com padrões de arquivos a serem ignorados

git clone <https do repo>
clona o repositório para o computador

git branch <nome do branch>
cria um novo branch, usado frequentemente para desenvolver novas funcionalidades em paralelo sem quebrar o master branch

git branch: mostra o nome dos branches disponíveis

git checkout <nome do branch>, troca o branch para o escolhido

git merge <nome do branch>: junta o branch escolhido ao master


#### Cocoapods
Instalar: (terminal) 
> sudo gem install cocoapods
> pod setup --verbose

Add cocoapods no projeto: fecha xcode, na pasta do proj. 
no terminal:
> pod init (cria o podfile)
> open -a Xcode Podfile (abre o podfile no xcode)
- uncomment next line
- adiciona pods no bloco do-end: pod 'NomeDoPod'
> pod install
- A partir daqui trabalhar com o .xcworkspace


### MVC
Model View Controller é um padrão de arquitetura de software

Model é a estrutura que controla os dados, mas não é o próprio dados. Manipula e lê dados.
Controller é a comunicação entre o Model e o View. Troca dados com o Model e envia dados para o View
View é a camada de interação com o usuário. É utilizada para receber a entrada de dados e apresentar visualmente o resultado.
No projeto do XCode, criar 3 pastas com cada nome e colocar dentro das pastas:
Model: SeuModel.swift; SeuBancoDeDados.swift
View: Main.storyboard; Images.xcasset
Controller: AppDelegate.swift; ViewController.swift


### Criar App Icon
www.canva.com para desenhar seu ícone
clica em custom dimension (1024x1024)
download como PNG

www.appicon.co para modificar para múltiplas dimensões
arrastar imagem gerada
escolher os dispositivos

no Xcode botão direito em Asses.Xcassets
apagar a pasta AppIcon.appiconset e colocar sua baixada de appicon.co


## UI Elements

### Constrains
Duas formas de criar restrições: pinning(fixação) ou alignment(alinhamento)

#### Pinning
Fixamos as bordas do objeto em relação as bordas da tela (ou outros objetos próximos), o tamanho é determinado dinamicamente, pela fórmula:
* width: tela.width - (x + x) , onde x é a distância da borda do objeto até as bordas da tela
* height: tela.height - (y + y) , onde y é a distância da borda do objeto até as bordas da tela

#### Alignment
Fixamos o tamanho do objeto (width e height) e decidimos o alinhamento (ex: centro da tela ou centro de alguma subview),
a distância para as bordas serão determinadas dinamicamente, pela fórmula (no caso do objeto no centro da tela):
* x: tela.width/2 - width/2
* y: tela.height/2 - height/2

-> PINNING NA PRÁTICA: o tamanho do objeto vai variar a depender do tamanho da tela do telefone.
- Clicar no botão Add New Constrains
- Remover fixar da margem: faz com que fixe a partir da borda da tela e não deixa margem
- Escolher distâncias 
- Add Constrains

-> ALIGNMENT NA PRÁTICA: mesmo tamanho para todas as telas, mas a distância para os outros objetos varia.
- Clicar no botão Constrains
- Clicar em width e height (para fixar tamanho)
- Clica no botão Align
- Escolhe alinhamento

-> DICA: ADICIONAR OBJETOS DENTRO DE CONTAINERS (UIViews) PARA FACILITAR ALINHAMENTO. (ex: 3 containers, os de baixo e de cima fixados nas margens e no do meio. O do meio alinhado no centro)

-> REMOVER CONTRAINS: Clica em Resolve Auto Layout Issues; Clear Constrains

-> IPHONE X: 1. Change the canvas to iPhone Xs. 2. Select the background view 3. With the background still selected, go to the size inspector and double click on the constraint that's called "Bottom Space to". 4. Change the first dropdown to Superview and the constant to 0.


#### Programaticamente
Criar um objeto square a ser localizado no centro da tela, independente do tamanho:
```
let square = UIView(frame: CGRect(x:self.view.frame.width/2 - self.width/2, y:self.view.frame.height/2 - self.height/2, width:100, height:100))
self.view.addSubview(square)
```

### Optionals
Em algumas ocasiões podemos querer que as variáveis possam tem valor **nil**. Para isso usamos optionals
A interrogação quer dizer: a variável nome pode ser **String** ou **nil**
```
let nome: String?
```
Se usar a variável sem ter inicializado, ocorrerá erro
A exclamação (_force unwrapping_) seria o programador dizendo: pode rodar o programa que eu garanto que a variável tem valor<br>
```print(nome!)```  erro de ponteiro nulo
<br>
para contornar esse erro pode ser usado:
```
if nome != nil
print(nome)
```
ou melhor: usar um _optional binding_
```
if let nomeCadastrado = nome
print(nome)
```

### Segue

Serve para trocar de ViewController e passar informações de um ViewControllers para outro (criando novos objetos de VC para isso)

1- Adiciona ViewController, ele não vai ter uma classe linkada automaticamente
2- Criar novo Swift File (ex: SecondViewController)
3- Clica na bola amarela em cima da tela, clica em Identity Inspector
4- Preenche a Class com o nome do arquivo criado (isso linka automaticamente o View ao Código)

###### Criar uma Segue a partir de um objeto:
1- Control no objeto e arrasta para outra tela
2- No ViewController:
````
    @IBOutlet weak var myText: UITextField!
    
    override func viewDidLoad() {
        super.viewDidLoad()
    }
    override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
        let destinationVC = segue.destination as! SecondViewController
        destinationVC.textPassedOver = myText.text!
    }
````
3- Na Second View:
```
    @IBOutlet weak var textPassed: UILabel!
    var textPassedOver = ""
    override func viewDidLoad() {
        super.viewDidLoad()
        textPassed.text = textPassedOver
    }
```

###### Criar uma Segue de uma tela para outra (desencadeada por algum objeto):
1- Control na bola amarela (ViewController) e arrasta para outra tela
2- Nomear o identifier (ex: goToSecondScreen)
3- No ViewController:
```
@IBOutlet weak var myText: UITextField!
    
    override func viewDidLoad() {
        super.viewDidLoad()
    }
    
    @IBAction func buttonPressed(_ sender: Any) {
        performSegue(withIdentifier: "goToSecondScreen", sender: self)
    }
    
    override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
        if segue.identifier == "goToSecondScreen"{
            let destinationVC = segue.destination as! SecondViewController
            destinationVC.textPassedOver = myText.text!
        }
    }
```

4- Na SecondView:
```
    @IBOutlet weak var textPassed: UILabel!
    var textPassedOver = ""
    override func viewDidLoad() {
        super.viewDidLoad()
        textPassed.text = textPassedOver
    }
```
-> ATENÇÃO: CASO SEJA NECESSÁRIO TROCAR INFORMAÇÕES ENTRE TELAS (IDA E VOLTA) NÃO É RECOMENDADO USAR SEGUES, POIS A CADA TROCA DE TELA, É CRIADO UM NOVO OBJETO VIEW CONTROLLER. NESSE CASO, DEVEMOS USAR DELEGATES E PROTOCOLOS 


### Protocols and Delegate
Usados para trocar informações entre telas. 
Delegate é um padrão usado quando precisamos que um objeto se responsabilize pelo recebimento das informações de outro objeto ou que realize alguma ação por ele. Fornece a possibilidade de comunicação entre seu objeto e um objeto previamente escrito (ex: CoreLocationManager)

Como fazer um protocolo
1) Escrever o protocolo (pode ser em arquivo separado) e as funções obrigatórias
```
protocol DelegateProtocolName {
  func delegateMethodName(nome: String) // no exemplo a funcão recebe uma string
}
```
2) Na classe que vai se "responsabilizar" por receber a informação, ou seja, vai ser a delegate
2.1 conform to protocol
2.2 implementar o delegaten Method
```
class ViewController: UIViewController, DelegateProtocolName { <- conform to protocol

  func delegateMethod(nome: String){
    myLabel.text = nome

  }
}
```
3) Na outra view:
```
var delegate: DelegateProtocolName?

```
4) Colocar o ViewController como delegate
```
override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
        if segue.identifier == "goToSecondScreen"{
            let destinationVC = segue.destination as! SecondViewController
            destinationVC.textPassedOver = myText.text!
            destinationVC.delegate = self
        }
    }
````
5) Chamar o delegateMethod
```
@IBAction func button2Pressed(_ sender: Any) {

    delegate?.dataReceived(data: text2.text!)
    dismiss(animated: true, completion: nil)
}
```

### Navigation Controller

Quando seu app contém várias telas, usar um navigation controller cria automaticamente uma barra de navegação na parte superior da tela com botão de voltar e permitindo deslizar de volta para a tela inicial.
> Clica na primeira tela -> Editor -> Embed In -> Navigation Controller

Se não quiser que determinada tela faça parte do navigation, mas só apareça como um pop-up, mudar o tipo de _Segue_ para *Present Modaly*

### TableViewCell

É um padrão de design formado por várias cells , cada uma compõe uma row. (Presente nos Ajustes do iPhone)

Conform to protocol: UITableViewDelegate e UITableViewDataSource, marcar a view como delegate através de um Outlet
Exige duas funções: numberOfRowsInSection e cellForRowsAt

Para criar uma cell customizada -> Criar um novo Cocoa Class File, subclass da UITableViewCell e marcar a opção: criar um .xib file.

> 1) cellforRowsAt :
```
let cell = tableView.dequeueReusableCell identifier: <"colocar o Identifier da cell customizada"> for: indexPath as! classe da CustomCell

return cell
```
> 2) definir a quantidade de rows
```
tableView(numberOfRowsInSection) -> Int
```
> 3) Tem que registrar a celula customizada
 ```
 messageTableView.register(UINib(nibName: "nome", bundle:nil), forCellReuseIdentifier:"identifier da cell")
 ```
 >4) Para configurar a altura da *row* :
 ```
 messageTableView.rowHeight = UITableView.automaticdimension
 messageTableView.estimatedRowHeight = 120.0
 ```
 
 #### TableViewCellController
    Quando a classe é subclasse da UITableViewController, já "ganhamos de graça:"
    - register
    - outlet
    - delegate
    Mas ainda é obrigatório as duas funções
     
 
 ### Animate
 
 Para animar mudança de tamanho ou posição
 ```
 UIView.animate(withDuration:0.6) {           // tempo em segundos
    code, exemplo:
    self.heightConstraint.constant = 300
    self.view.layoutIfNeeded()                // reseta o layout para mostrar as mudanças
 }
```

### TapGesture
1) adiciona a classe: UITableViewDelegate
2) na viewDidLoad:
```
let tapGesture = UIGestureRecognizer(target: self, action:#selector(myFunc))
myTableView.addGestureRecognizer(tapGesture)
````
3) Definir a função:
```
@objc func myFunc(){
print("tableView tapped")
}
```

#### SAVE/RETRIEVE FROM FIREBASE

1 - Save)
```
let messageDB = Database.database().reference.child("NomeDoDB")
let myMessage = escolher o que quer salvar
messageDB.childByAutoID.setvalue(myMessage) { (error, reference) in
if error != nil{
  print(error!)
} else {
  fazer o que quiser... habilitar botão, etc...
  zerar textField
}
}
```
2-Retrieve)
```
let messageDB = Database.database().reference.child("NomeDoDB")
messageDB.observe(.childAdded) { (snapshot) in
            let snapshotValue = snapshot.value as! Dictionary<String,String>
            let text = snapshotValue["MessageText"]!
            let sender = snapshotValue["Sender"]!
            
            let message = Message()
            message.messageText = text
            message.sender = sender
            
            self.messageArray.append(message)
            self.messageTableView.reloadData()
            self.designTableView()
```


### Alert
```
let alert = UIAlertController(title: "titulo", message: "mensagem", preferredStyle:.alert)
let action = UIAlertAction(title:"confirm", style:.default) { (action) in
    code : salvar? o que fazer após o clique em confir?
    print(textField.text!)
}
alert.addAction(action)
let textField = UITextField()
alert.addTextFiel(alertTextField){
alertTextField.placeholder = "New Item"
textField = alertTextField
}
```

### DATA PERSISTENCE

#### User Defaults

Serve para armazenar dados em pouca quantidade. Toda vez que o app é aberto, todos os dados presentes no user defaults são carregados, por esse motivo não é recomendável salvar muitos dados. Bastante usado para salvar preferências do usuário.
UserDefaults can save integers, booleans, strings, arrays, dictionaries, dates and more, but you should be careful not to save too much data because it will slow the launch of your app. SÓ SALVA TIPOS PRIMITIVOS
```
let defaults = UserDefaults.standard
defaults.set(25, forKey: "Age")
defaults.set(true, forKey: "UseTouchID")
defaults.set(CGFloat.pi, forKey: "Pi")
defaults.set("Paul Hudson", forKey: "Name")
defaults.set(Date(), forKey: "LastRun")
```
Para restaurar:
```
let age = defaults.integer(forKey: "Age")
let useTouchID = defaults.bool(forKey: "UseTouchID")
let pi = defaults.double(forKey: "Pi")
let savedArray = defaults.object(forKey: "SavedArray") as? [String] ?? [String]()
```

#### NSEncoder
Forma mais 'robusta' do que o userDefaults para salvar dados. Assim como o userDefaults, os dados ficam armazenados no SandBox e são sincronizados automaticamente com o iCloud. Além dos tipos primitivos, tb pode salvar classes criadas, porém essas classes só podem conter tipos primitivos
```
let dataFilePath = FileManager.default.urls(for: .documentDirectory, in: .userdomainMask).first?.appendingPathComponent("Items.plist")

let encoder = PropertyListEncoder()

do{
  let data = try encoder.encode(itemArray)
  try data.write(to: dataFilePath)
} catch{
  print("Error encoding \(error)")
}
```
#### NSDECODER
```  
func loadItems(){
        if let data = try? Data(contentsOf: dataFilePath!) {
            let decoder = PropertyListDecoder()
            do {
                itemArray = try decoder.decode([Item].self, from: data)
            } catch {
                print("Error decoding: \(error)")
            }
        }
        
    }
````

#### CORE MODEL
Quando for criar o projeto, marcar *usar core data*
Caso o projeto já tenha sido iniciado, para adicionar o Core Model
1) Criar um novo arquivo tipo Data Model (na verdade é um banco de dados SQLite)
2) Criar um novo projeto de teste só para pegar as funções do AppDelegate
3) Mudar o nome do appDelegate para o nome do seu model
4) Criar uma variável para acessar o contexto a partir do seu Controller
```
let context = (UIApplication.shared.delegate as! App Delegate).persistentContainer.viewContext
```
5) Seu banco de dados fica salvo em:
```print(FileManager.default.urls(for: .documentDirectory, in: .userDomainMask))```
6) No banco de dados, criar uma Entity(classe) e seus atributos (properties) 

##### Crud

1) criar um objeto do seu banco de dados, obrigatório criar seus atributos caso eles não sejam opcionais ex:
```
let newItem = Item(context: context)
newItem.title = "exemplo de Item"
newItem.done = false
```
2)Salvar o contexto
```
do {
try context.save()
} catch {
print("Error saving context \(error)")
}
```
