```swift
//
//  ContentView.swift
//  ImageModifiers
//
//  Created by paige on 2021/12/19.
//

import SwiftUI

struct ContentView: View {
    var body: some View {

        ScrollView {

            Image("image1")
                .resizable()
                .aspectRatio(contentMode: .fit)
                .padding()

            Image(systemName: "faceid")
                .font(.largeTitle)
                .padding()

            Image(systemName: "wifi")
                .imageScale(.large)
                .foregroundColor(.red)
                .frame(width: 100, height: 100)
                .background(.black)
                .font(.system(size: 50))
                .padding()

            Image(systemName: "person.icloud.fill")
                .font(.system(size: 50))
                .blur(radius: 3)
                .foregroundColor(.red)

        }



    }

}

struct GridImage: View {

    var body: some View {
        VStack {
            List {
                ForEach(0..<10) { _ in
                    HStack {
                        ForEach(0..<3) {_ in
                            Image("image2")
                                .resizable()
                                .scaledToFit()
                        }
                    }
                }
            }
        }
    }

}

struct ImageBackground: View {

    var body: some View {
        VStack {
            Image("image2")
                .resizable()
                .aspectRatio(contentMode: .fill)
                .edgesIgnoringSafeArea(.all)
        }
    }

}

struct NetworkImage: View {

    @State private var img: UIImage? = nil
    let staticImage = UIImage(named: "image1")

    var body: some View {
        Image(uiImage: self.img ?? staticImage!)
            .resizable()
            .onAppear(perform: imageDownloader)
            .frame(width: 400, height: 400, alignment: .center)
            .onTapGesture {
                //run some code
                print("Image was tapped")
            }
    }

    func imageDownloader() {
        guard let imgURL = URL(string: "https://womenandtravel.net/wp-content/webp-express/webp-images/uploads/2021/06/hot-korean-girls-e1624449716581-500x359.jpg.webp") else {
            return
        }
        URLSession.shared.dataTask(with: imgURL) { data, response, error in
            if let imageData = data, let imageToDisplay = UIImage(data: imageData) {
                self.img = imageToDisplay
            } else {
                print("error: \(String(describing: error))")
            }
        }.resume()
    }

}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}
```
