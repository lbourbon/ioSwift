# ioSwift

## Novo Projeto
Organization Identifier: com.[nome da empresa]

## Criar App Icon

www.canva.com para desenhar seu ícone
clica em custom dimension (1024x1024)
download como PNG

www.appicon.co para modificar para múltiplas dimensões
arrastar imagem gerada
escolher os dispositivos

no Xcode botão direito em Asses.Xcassets
apagar a pasta AppIcon.appiconset e colocar sua baixada de appicon.co

## Constrains



## Cocoapods
instalar: terminal > sudo gem install cocoapods
                  > pod setup --verbose
adic cocoapods no projeto: fecha xcode,
na pasta do proj. no terminal > pod init (cria o podfile)
> open -a Xcode Podfile (abre o podfile no xcode)
- uncomment next line
- adiciona pods no bloco do-end: pod 'NomeDoPod'
> pod install
- A partir daqui trabalhar com o .xcworkspace
