# Week-8

### **REACT JS**

#### **Context**
Context memungkinkan pengiriman data melalui pohon komponen tanpa meneruskan alat peraga secara manual di setiap level.<br/>

Dalam aplikasi React, kami mengirimkan data dengan pendekatan top-down melalui props. Kadang-kadang tidak nyaman untuk jenis props tertentu yang dibutuhkan oleh banyak komponen dalam aplikasi React. Context menyediakan cara untuk meneruskan nilai antar komponen tanpa secara eksplisit meneruskan penyangga melalui setiap level pohon komponen.<br/>

Cara menggunakan context:
1. Ada dua langkah utama untuk menggunakan context React ke dalam aplikasi React
2. Siapkan penyedia context dan tentukan data yang ingin Anda simpan.
Gunakan konsumen context kapan pun Anda membutuhkan data dari toko

Context digunakan untuk berbagi data yang dapat dianggap "global" untuk pohon komponen Bereaksi dan menggunakan data tersebut jika diperlukan, seperti pengguna yang diautentikasi saat ini, tema, dll. Misalnya, dalam cuplikan kode di bawah ini, kita secara manual melakukan thread melalui " theme" prop untuk menata komponen Button.

    class App extends React.Component {  
        render() {  
            return <Toolbar theme="dark" />;  
        }  
    }  
  
    function Toolbar(props) {  
        return (  
            <div>  
            <ThemedButton theme={props.theme} />  
            </div>  
        );  
    }  
  
    class ThemedButton extends React.Component {  
        render() {  
            return <Button theme={this.props.theme} />;  
        }  
    }  

Dalam kode di atas, komponen fungsi Toolbar mengambil tambahan "tema" prop dan meneruskannya ke ThemeButton. Ini bisa menjadi merepotkan jika setiap tombol di aplikasi perlu mengetahui tema karena harus melewati semua komponen. Tetapi dengan menggunakan konteks, kita dapat menghindari melewatkan props untuk setiap komponen melalui elemen perantara.<br/>

Kita dapat memahaminya dari contoh di bawah ini. Di sini, context meneruskan nilai ke pohon komponen tanpa secara eksplisit memasukkannya ke setiap komponen.

    // Create a context for the current theme which is "light" as the default.  
    const ThemeContext = React.createContext('light');  
  
    class App extends React.Component {  
        render() {  
            /* Use a ContextProvider to pass the current theme, which allows every component to read it, no matter how deep it is. Here, we are passing the "dark" theme as the current value.*/  
  
            return (  
            <ThemeContext.Provider      value="dark">  
                <Toolbar />  
            </ThemeContext.Provider>  
            );  
        }  
    }  
  
    // Now, it is not required to pass the theme down explicitly for every component.  
    function Toolbar(props) {  
        return (  
            <div>  
            <ThemedButton />  
            </div>  
        );  
    }  
  
    class ThemedButton extends React.Component {  
        static contextType =    ThemeContext;  
        render() {  
            return <Button theme={this.context} />;  
        }  
    }  

- React.createContext<br/>
  Ketika React merender komponen yang berlangganan ke objek konteks ini, maka ia akan membaca nilai konteks saat ini dari penyedia yang cocok di pohon komponen.

        const  MyContext = React.createContext(defaultValue); 
  
  Ketika sebuah komponen tidak memiliki Penyedia yang cocok di pohon komponen, ia mengembalikan argumen defaultValue. 
  
#### **React-Test**
Ada banyak jenis pengujian, tetapi yang utama dibagi menjadi 3, yaitu:
1. unit testing
2. integration testing
3. UI testing

Jest adalah pelari pengujian JavaScript, yaitu pustaka JavaScript untuk membuat, menjalankan , dan menyusun pengujian .<br/>
Jest dikirimkan sebagai paket NPM, Anda dapat menginstalnya di proyek JavaScript apa pun. Jest adalah salah satu test runner terpopuler saat ini , dan pilihan default untuk proyek React.

- Installasi Jest
  
        npm i jest --save-dev

    Kita juga mengonfigurasi skrip NPM untuk menjalankan pengujian kita dari baris perintah. Buka package.jsondan konfigurasikan skrip bernama testuntuk menjalankan Jest:

        "scripts": {
            "test": "jest"
        },

- Set Up React Testing
  - Installasi<br/>
    1. Set Up dengan Create React App
       
            npm install --save-dev react-test-renderer
    2. Setup tanpa Buat Aplikasi React

            npm install --save-dev jest babel-jest @babel/preset-env @babel/preset-react react-test-renderer
       
       Package.json akan terlihat seperti ini (di mana ```<current-version>```nomor versi terbaru sebenarnya untuk paket tersebut). Silakan tambahkan skrip dan entri konfigurasi

            {
                "dependencies": {
                    "react": "<current-version>",
                    "react-dom": "<current-version>"
                },
                "devDependencies": {
                    "@babel/preset-env":                "<current-version>",
                    "@babel/preset-react":              "<current-version>",
                    "babel-jest":               "<current-version>",
                    "jest":     "<current-version>",
                    "react-test-renderer":              "<current-version>"
                },
                "scripts": {
                    "test": "jest"
                }
            }
        Dan pad Babel.config.js seperti berikut:

            module.exports = {
                presets: [
                    '@babel/preset-env',
                    ['@babel/preset-react',                 {runtime: 'automatic'}],
                ],
            };