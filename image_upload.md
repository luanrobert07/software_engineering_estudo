# 🌍 Image upload

------------------------

- [📜 Introdução a image upload](#-introdução-image-upload)
  - [📚 Como fazer?](#-como-fazer)
    - [React JS e Context API](#principais-conceitos-do-react)
    - [AWS com Node.js](#-componentes)
    - [React Native](#-jsx)

## 📚 Como fazer:

### React JS e Context API
Passo 1 - Criando o projeto e estruturando as pastas
Crie o projeto com React usando create-react-app com TypeScript:

npx create-react-app upload-frontend-react-hooks --template typescript
Organize a estrutura de pastas, crie uma pasta src e dentro dela as pastas components, context, services e Styles:

https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8878dd38-f1e7-4537-aa6f-496a973a4610/Screen_Shot_2020-09-24_at_17.10.30.png
Passo 2 - Instalando as dependências do projeto
Seu arquivo package.json deve ter essas dependências, portanto, copie e cole as que estiverem faltando  no seu projeto e execute yarn install para instalar.

{
  "name": "upload-frontend-react-hooks",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "@testing-library/jest-dom": "^4.2.4",
    "@testing-library/react": "^9.3.2",
    "@testing-library/user-event": "^7.1.2",
    "@types/jest": "^24.0.0",
    "@types/lodash": "^4.14.161",
    "@types/node": "^12.0.0",
    "@types/react": "^16.9.0",
    "@types/react-dom": "^16.9.0",
    "@types/react-dropzone": "^5.1.0",
    "@types/styled-components": "^5.1.3",
    "@types/uuid": "^8.3.0",
    "axios": "^0.20.0",
    "filesize": "^6.1.0",
    "react": "^16.13.1",
    "react-circular-progressbar": "^2.0.3",
    "react-dom": "^16.13.1",
    "react-dropzone": "^11.1.0",
    "react-icons": "^3.11.0",
    "react-scripts": "3.4.3",
    "styled-components": "^5.2.0",
    "typescript": "~3.7.2",
    "uuid": "^8.3.0"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
  "eslintConfig": {
    "extends": "react-app"
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  }
}
Dependências:

As dependências que tem o prefixo: @types/ são as tipagens de cada biblioteca.

axios = para fazer requisições HTTP ao servidor;
filesize = mostrar de forma amigável o tamanho da imagem (2 MB, 4 GB, etc);
react-circular-progressbar = faz animação do progresso da imagem;
react-dropzone = fica ouvindo o envio de imagens no front end;
react-icons = ícones da aplicação;
styled-components = auxilia na criação e estilização de componentes;
uuid = gerador de IDs no formato UUID.
Essas são as bibliotecas externas necessárias para criar essa aplicação.

Para executar o projeto, na raiz do projeto:

yarn start
// ou
npm start
Passo 3 - Estilizando a aplicação
Na pasta styles, crie o arquivo global.ts. Como o nome sugere, nesse arquivo terá toda estilização global do App:

01: import { createGlobalStyle } from "styled-components";
02: 
03: import "react-circular-progressbar/dist/styles.css";
04: 
05: export default createGlobalStyle`
06:   * {
07:     margin: 0;
08:     padding: 0;
09:     outline: 0;
10:     box-sizing: border-box;
11:   }
12: 
13:   body {
14:     font-family: Arial, Helvetica, sans-serif;
15:     font-size: 14px;
16:     background: #7159c1;
17:     text-rendering: optimizeLegibility;
18:     -webkit-font-smoothing: antialiased;
19:   }
20: 
21:   html, body, #root {
22:     height: 100%;
23:   }
24: `;
01 - importa a função createGlobalStyle da lib styled-components

03 - a lib react-circular-progressbar pede para fazer a importação da estilização dos componentes;

05 a 25 - exporta a função que faz a estilização global de toda a aplicação. Nesse arquivo deve conter toda a configuração geral do CSS que será compartilhado em todo o App;

Esse componente será importado no arquivo App.tsx, que veremos mais para frente.

Passo 4 - Estilizando o componente pai — App.tsx
Crie o arquivo src/styles.ts que irá estilizar o componente App.tsx:

01: import styled from "styled-components";
02: 
03: export const Container = styled.div`
04:   height: 100%;
05:   display: flex;
06:   justify-content: center;
07:   align-items: center;
08: `;
09: 
10: export const Content = styled.div`
11:   width: 100%;
12:   max-width: 400px;
13:   margin: 30px;
14:   background: #fff;
15:   border-radius: 4px;
16:   padding: 20px;
17: `;
18:
01 - importa o styled-components;

03 a 08 - cria uma div com nome Container e sua estilização;

10 a 17 - cria uma div com nome Content que estiliza a área onde irá ficar o conteúdo da aplicação;

Passo 5 - Criando o componente App.tsx — a raiz da aplicação React
Substitua o conteúdo do arquivo App.tsx por esse:

01: import React from "react";
02: 
03: import GlobalStyle from "./styles/global";
04: import { Container, Content } from "./styles";
05: 
06: import Upload from "./components/Upload";
07: import FileList from "./components/FileList";
08: 
09: import { FileProvider } from "./context/files";
10: 
11: const App: React.FC = () => (
12:   <FileProvider>
13:     <Container>
14:       <Content>
15:         <Upload />
16:         <FileList />
17:       </Content>
18:       <GlobalStyle />
19:     </Container>
20:   </FileProvider>
21: );
22: 
23: export default App;
24:
01 - Todo arquivo React que utiliza sintaxe (jsx ou tsx)<ComponentX /> deve conter a importação do React;

03 - Importa a função createGlobalStyle e nomeamos como GlobalStyle do arquivo global.ts;

04 - Importa os componentes de estilização Container e Content do arquivo styles.ts;

06 e 07 - Importa os dois componentes da aplicação: Upload, que tem o dropzone onde vamos enviar os arquivos, e FileList, que é a listagem dos arquivos. Esses arquivos serão criados ao longo do tutorial;

09 - Importa FileProvider, que é o contexto que armazena o estado de cada imagem que será enviada na aplicação e controla as ações sobre esse estado;

11 a 23 - Cria um componente funcional App passando o FileProvider como componente raiz da aplicação, com isso o contexto será compartilhado entre os componentes filhos, netos, bisnetos... ou seja, tudo que estiver abaixo desse arquivo. Não precisamos ficar passando props, evitando assim o Prop Drilling;

13 - Adiciona o componente estilizado Container que estiliza a raiz da aplicação;

14 -  Adiciona o componente estilizado Content que recebe como conteúdo os dois componentes Upload e FileList;

23 - Exporta o App que será utilizando no arquivo index.ts, o qual irá renderizar o App.tsx com seus respectivos filhos no Front End.


Passo 6 - Criando o serviço de requisições HTTP com Axios
Para consumir a API do back end iremos utilizar o Axios.

Na pasta services vamos criar o arquivo api.ts:

import axios from "axios";

const api = axios.create({
  baseURL: "<http://localhost:3000>",
});

export default api;
O código é bem simples, lendo esse post você tem um overview sobre o Axios.

Passo 7 - Criando o componente de Upload
Vamos criar a parte visual do upload de arquivos.

Crie a pasta Upload e o arquivo styles.ts: components/Upload/styles.ts

01: import styled, { css } from "styled-components";
02: 
03: const dragActive = css`
04:   border-color: #78e5d5;
05: `;
06: 
07: const dragReject = css`
08:   border-color: #e57878;
09: `;
10: 
11: type IDropContainer = {
12:   isDragActive?: boolean;
13:   isDragReject?: boolean;
14: };
15: 
16: export const DropContainer = styled.div<IDropContainer>`
17:   border: 1px dashed #ddd;
18:   border-radius: 4px;
19:   cursor: pointer;
20: 
21:   transition: height 0.2s ease;
22: 
23:   ${(props: any) => props.isDragActive && dragActive};
24:   ${(props: any) => props.isDragReject && dragReject};
25: `;
26: 
27: const messageColors = {
28:   default: "#999",
29:   error: "#e57878",
30:   success: "#78e5d5",
31: };
32: 
33: interface ITypeMessageColor {
34:   type?: "default" | "error" | "success";
35: }
36: 
37: export const UploadMessage = styled.p<ITypeMessageColor>`
38:   display: flex;
39:   color: ${(props) => messageColors[props.type || "default"]};
40:   justify-content: center;
41:   align-items: center;
42:   padding: 15px 0;
43: `;
Linha: 33 - Criamos a interface ITypeMessageColor, que tem a propriedade opcional type, com os tipos possíveis: default, error ou success, e aplicamos na linha 37, para a IDE e o código entenderem o props.type.

Nosso foco está na lógica e, para ganhar tempo, não vamos explicar a estilização aqui, caso você queira entender cada propriedade CSS, veja o vídeo dessa implementação.

Passo 8 - Criando a lógica e estilização do Upload
Na pasta Upload crie o arquivo index.tsx: components/Upload/index.tsx

01: import React, { useCallback } from "react";
02: import { useDropzone } from "react-dropzone";
03: import { useFiles } from "../../context/files";
04: 
05: import { DropContainer, UploadMessage } from "./styles";
06: 
07: function Upload() {
08:   const { handleUpload } = useFiles();
09: 
10:   const onDrop = useCallback(
11:     (files) => {
12:       handleUpload(files);
13:     },
14:     [handleUpload]
15:   );
16: 
17:   const {
18:     getRootProps,
19:     getInputProps,
20:     isDragActive,
21:     isDragReject,
22:   } = useDropzone({
23:     accept: ["image/jpeg", "image/pjpeg", "image/png", "image/gif"],
24:     onDrop,
25:   });
26: 
27:   const renderDragMessage = useCallback(() => {
28:     if (!isDragActive) {
29:       return <UploadMessage>Arraste imagens aqui...</UploadMessage>;
30:     }
31: 
32:     if (isDragReject) {
33:       return (
34:         <UploadMessage type="error">
35:           Tipo de arquivo não suportado
36:         </UploadMessage>
37:       );
38:     }
39: 
40:     return <UploadMessage type="success">Solte as imagens aqui</UploadMessage>;
41:   }, [isDragActive, isDragReject]);
42: 
43:   return (
44:     <DropContainer {...getRootProps()}>
45:       <input {...getInputProps()} />
46:       {renderDragMessage()}
47:     </DropContainer>
48:   );
49: }
50: 
51: export default Upload;

02 - Importa o hook useDropzone que lida com dropzone de arquivos;

03 - Importa o custom hook useFiles do contexto que iremos criar logo mais;

05 - Importa a estilização do componente, que criamos no passo anterior;

07 - Cria a função Upload;

08 - Disponibiliza a função handleUpload que vem do contexto do useFiles();

10 a 15 - Cria a função onDrop que recebe os arquivos (files) que são enviados no front end, invoca a função handleUpload para lidar com o upload do arquivo que está implementado no contexto no arquivo files.tsx e passa files como argumento;

17 a 25 - O hook useDropzone recebe um objeto de configuração aceitando a propriedade accept com um array de tipos de arquivos que podem ser enviados pelo o usuário e serão aceitos. Recebe também a função onDrop (que criamos nas linhas 10 a 15) como segundo parâmetro. Ela devolve, via desestruturação, as funções getRootProps e getInputProps, e as duas variáveis booleanas: isDragActive, que indica se está sendo enviado algum arquivo no dropzone, e isDragReject, que muda para true se o arquivo "dropado" é aceito ou false para rejeitado. Conforme a configuração da propriedade Accept;

27 a 41 - Cria a função renderDragMessage que implementa a lógica de como será exibido o dropzone. A primeira condição verifica se o isDragActive não tem arquivos arrastados no componente, retorna o componente UploadMessage que é uma tag <p> do HTML estilizado com sua respectiva mensagem;

Na linha 32, se o arquivo foi rejeitado, é enviado a prop error e o texto será alterado. Por fim, na linha 40 retorna o texto de sucesso, pois o isDragActive estará true e isDragReject estará false, ou seja, o arquivo pode ser solto no dropzone. Essa função está envolvida em um useCallback e recebe as variáveis isDragActive e isDragReject como dependência;

43 a 49: retorna o componente estilizado DropContainer (div) que recebe as propriedades do dropzone. Nessa div está o input do HTML com as propriedades do dropzone e, por fim, a função renderDragMessage é invocada, renderizando o texto de acordo com a lógica que explicamos na linha 27 a 41 acima;

51: Exporta o componente Upload para ser usado no App.tsx.

https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3ad7725c-d1b3-46a0-8480-78ba307094d8/Screen_Shot_2020-10-05_at_20.32.01.png
Passo 9 - Criando o componente de Listagem de Arquivos importados
Na pasta components crie a pasta FileList com os arquivos index.tsx e styles.ts

No arquivo styles.ts adicione o código da estilização:

import styled from "styled-components";

export const Container = styled.ul`
  margin-top: 20px;

  li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: #444;

    & + li {
      margin-top: 15px;
    }
  }
`;

export const FileInfo = styled.div`
  display: flex;
  align-items: center;

  div {
    display: flex;
    flex-direction: column;

    span {
      font-size: 12px;
      color: #999;
      margin-top: 5px;

      button {
        border: 0;
        background: transparent;
        color: #e57878;
        margin-left: 5px;
        cursor: pointer;
      }
    }
  }
`;

interface PreviewProps {
  src?: string;
}

export const Preview = styled.div<PreviewProps>`
  width: 36px;
  height: 36px;
  border-radius: 5px;
  background-image: url(${(props) => props.src});
  background-repeat: no-repeat;
  background-size: cover;
  background-position: 50% 50%;
  margin-right: 10px;
`;
O componente estilizado Container é uma li do HTML com sua respectiva estilização.

FileInfo contém toda estilização das tags HTML que vamos utilizar no index.tsx.

Preview é uma div estilizada que mostra uma pequena imagem do arquivo enviado.

Passo 10 - Criando a lógica da listagem de arquivos importados
No arquivo index.tsx, que foi criado no passo anterior, adicione esse código:

components/FileList/index.tsx

01: import React from "react";
02: import { CircularProgressbar } from "react-circular-progressbar";
03: import { MdCheckCircle, MdError, MdLink, MdMoodBad } from "react-icons/md";
04: import { useFiles } from "../../context/files";
05: import { IFile } from "../../context/files";
06: 
07: import { Container, FileInfo, Preview } from "./styles";
08: 
09: const FileList = () => {
10:   const { uploadedFiles: files, deleteFile } = useFiles();
11: 
12:   if (!files.length)
13:     return (
14:       <span>
15:         <MdMoodBad
16:           style={{ marginLeft: "45%", marginTop: 10 }}
17:           size={24}
18:           color="#d5d2d2"
19:         />
20:       </span>
21:     );
22: 
23:   return (
24:     <Container>
25:       {files.map((uploadedFile: IFile) => (
26:         <li key={uploadedFile.id}>
27:           <FileInfo>
28:             <Preview src={uploadedFile.preview} />
29:             <div>
30:               <strong>{uploadedFile.name}</strong>
31:               <span>
32:                 {uploadedFile.readableSize}{" "}
33:                 {!!uploadedFile.url && (
34:                   <button onClick={(e) => deleteFile(uploadedFile.id)}>
35:                     Excluir
36:                   </button>
37:                 )}
38:               </span>
39:             </div>
40:           </FileInfo>
41: 
42:           <div>
43:             {!uploadedFile.uploaded && !uploadedFile.error && (
44:               <CircularProgressbar
45:                 styles={{
46:                   root: { width: 24 },
47:                   path: { stroke: "#7159c1" },
48:                 }}
49:                 strokeWidth={10}
50:                 text={String(uploadedFile.progress)}
51:                 value={uploadedFile.progress || 0}
52:               />
53:             )}
54: 
55:             {uploadedFile.url && (
56:               <a
57:                 href={uploadedFile.url}
58:                 target="_blank"
59:                 rel="noopener noreferrer"
60:               >
61:                 <MdLink style={{ marginRight: 8 }} size={24} color="#222" />
62:               </a>
63:             )}
64: 
65:             {uploadedFile.uploaded && (
66:               <MdCheckCircle size={24} color="#78e5d5" />
67:             )}
68:             {uploadedFile.error && <MdError size={24} color="#e57878" />}
69:           </div>
70:         </li>
71:       ))}
72:     </Container>
73:   );
74: };
75: 
76: export default FileList;
02 - Importa o componente CircularProgress que contém toda estilização e lógica para exibir o loading de progresso;

03 - Importa os ícones de status e ação do usuário;

04 -Importa o useFiles que é o contexto que contém o estado e funções dos arquivos enviados;

05 - Importa a interface IFile que é a representação do objeto File (que será criado logo mais adiante);

07 - Importa os componentes estilizados que foram criados no passo anterior;

09 - Cria o componente funcional FileList ;

10 - Acessa a variável uploadedFiles renomeando para files e acessa a função deleteFile, ambas do contexto useFiles;

12 a 21 - É feito uma verificação condicional que renderiza um ícone representando que a lista está vazia;

23 a 73 - Retorna um container que possui seus componentes filhos. É feito um loop usando o map do array files para criar um componente para cada arquivo enviado, mostrando seu preview (imagem), nome do arquivo, tamanho em MB e a URL para acessar o arquivo;

34 - O componente tem um botão que, quando clicado, chama a função deleteFile;

43 a 53 - Componente CircularProgressbar é exibido enquanto o arquivo não foi enviado (uploaded = false) ou se não ocorreu algum erro;

55 - URL do arquivo é exibida assim que ela recebida do servidor;

65 - Quando finaliza o upload, o loading de progresso para de aparecer e aparece um ícone representando o status de finalizado no lugar do loading;

76 - Exportamos o componente para ser utilizado no App.tsx

Repare que é um componente que não possui comportamento, ele apenas recebe o estado e funções que alteram o estado via hook do contexto. Isso é um plus no componente, pois sua responsabilidade é renderizar os componentes e invocar funções, e o contexto que lida com lógica da manipulação de estado e o comportamento das funções.

https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6dcc514a-53ce-4cb9-b24a-c338503b3b41/Screen_Shot_2020-10-05_at_20.33.07.png
Passo 11 - Criando o contexto que armazena o estado dos arquivos enviados
Na pasta context crie o arquivo files.tsx: src/context/files.tsx. Copie e cole o código abaixo.

Nesse código estamos criando o hook de contexto usando a Context API do React, ela será responsável por pegar os dados do back end usando o serviço API que criamos no passo 5. Armazenar esses valores no estado uploadedFiles e fazer a manipulação no estado conforme as ações do usuário de inserir nova imagem via upload ou deletar um arquivo.

Leia o código abaixo e, em seguida, os comentários de cada trecho relevante.

001: import React, {
002:   createContext,
003:   useState,
004:   useEffect,
005:   useCallback,
006:   useContext,
007: } from "react";
008: import { v4 as uuidv4 } from "uuid";
009: import filesize from "filesize";
010: 
011: import api from "../services/api";
012: 
013: export interface IPost {
014:   _id: string;
015:   name: string;
016:   size: number;
017:   key: string;
018:   url: string;
019: }
020: 
021: export interface IFile {
022:   id: string;
023:   name: string;
024:   readableSize: string;
025:   uploaded?: boolean;
026:   preview: string;
027:   file: File | null;
028:   progress?: number;
029:   error?: boolean;
030:   url: string;
031: }
032: 
033: interface IFileContextData {
034:   uploadedFiles: IFile[];
035:   deleteFile(id: string): void;
036:   handleUpload(file: any): void;
037: }
038: 
039: const FileContext = createContext<IFileContextData>({} as IFileContextData);
040: 
041: const FileProvider: React.FC = ({ children }) => {
042:   const [uploadedFiles, setUploadedFiles] = useState<IFile[]>([]);
043: 
044:   useEffect(() => {
045:     api.get<IPost[]>("posts").then((response) => {
046:       const postFormatted: IFile[] = response.data.map((post) => {
047:         return {
048:           ...post,
049:           id: post._id,
050:           preview: post.url,
051:           readableSize: filesize(post.size),
052:           file: null,
053:           error: false,
054:           uploaded: true,
055:         };
056:       });
057: 
058:       setUploadedFiles(postFormatted);
059:     });
060:   }, []);
061: 
062:   useEffect(() => {
063:     return () => {
064:       uploadedFiles.forEach((file) => URL.revokeObjectURL(file.preview));
065:     };
066:   });
067: 
068:   const updateFile = useCallback((id, data) => {
069:     setUploadedFiles((state) =>
070:       state.map((file) => (file.id === id ? { ...file, ...data } : file))
071:     );
072:   }, []);
073: 
074:   const processUpload = useCallback(
075:     (uploadedFile: IFile) => {
076:       const data = new FormData();
077:       if (uploadedFile.file) {
078:         data.append("file", uploadedFile.file, uploadedFile.name);
079:       }
080: 
081:       api
082:         .post("posts", data, {
083:           onUploadProgress: (progressEvent) => {
084:             let progress: number = Math.round(
085:               (progressEvent.loaded * 100) / progressEvent.total
086:             );
087: 
088:             console.log(
089:               `A imagem ${uploadedFile.name} est√° ${progress}% carregada... `
090:             );
091: 
092:             updateFile(uploadedFile.id, { progress });
093:           },
094:         })
095:         .then((response) => {
096:           console.log(
097:             `A imagem ${uploadedFile.name} j√° foi enviada para o servidor!`
098:           );
099: 
100:           updateFile(uploadedFile.id, {
101:             uploaded: true,
102:             id: response.data._id,
103:             url: response.data.url,
104:           });
105:         })
106:         .catch((err) => {
107:           console.error(
108:             `Houve um problema para fazer upload da imagem ${uploadedFile.name} no servidor AWS`
109:           );
110:           console.log(err);
111: 
112:           updateFile(uploadedFile.id, {
113:             error: true,
114:           });
115:         });
116:     },
117:     [updateFile]
118:   );
119: 
120:   const handleUpload = useCallback(
121:     (files: File[]) => {
122:       const newUploadedFiles: IFile[] = files.map((file: File) => ({
123:         file,
124:         id: uuidv4(),
125:         name: file.name,
126:         readableSize: filesize(file.size),
127:         preview: URL.createObjectURL(file),
128:         progress: 0,
129:         uploaded: false,
130:         error: false,
131:         url: "",
132:       }));
133: 
134:       // concat é mais performático que ...spread
135:       // <https://www.malgol.com/how-to-merge-two-arrays-in-javascript/>
136:       setUploadedFiles((state) => state.concat(newUploadedFiles));
137:       newUploadedFiles.forEach(processUpload);
138:     },
139:     [processUpload]
140:   );
141: 
142:   const deleteFile = useCallback((id: string) => {
143:     api.delete(`posts/${id}`);
144:     setUploadedFiles((state) => state.filter((file) => file.id !== id));
145:   }, []);
146: 
147:   return (
148:     <FileContext.Provider value={{ uploadedFiles, deleteFile, handleUpload }}>
149:       {children}
150:     </FileContext.Provider>
151:   );
152: };
153: 
154: function useFiles(): IFileContextData {
155:   const context = useContext(FileContext);
156: 
157:   if (!context) {
158:     throw new Error("useFiles must be used within FileProvider");
159:   }
160: 
161:   return context;
162: }
163: 
164: export { FileProvider, useFiles };

001 a 011 - Importação dos códigos necessários

013 a 019 - Cria e exporta a interface IPost que define o formado do objeto que estará vindo da API;

021 a 031 - Cria e exporta a interface IFile que define o objeto e suas propriedades do arquivo;

033 a 037 - Cria a interface IFileContextData que define o formato do objeto do contexto;

039 - Cria o contexto FileContext utilizando a função createContext seguindo o contrato definido na interface IFileContextData;

041 a 152 - Cria o componente funcional FileProvider que recebe um children como parâmetro que são todas os componentes abaixo do FileProvider que definimos no App.tsx;

042 - O estado uploadFiles do tipo IFile[] que será manipulado pelo hook que estamos criando e será fornecido ao contexto no return;

044 a 060 - Cria um useEffect para buscar os dados do back end utilizando o axios, o valor é formatado. São adicionados alguns valores iniciais seguindo o contrato da interface IFile, uma vez que os dados vem do tipo IPost.  No final é adicionado na variável de estado uploadedFiles na linha 058. Essa função é executada assim que o componente monta em tela;

062 a 066 - Utiliza o useEffect para invocar a função de retorno assim que esse componente sair da tela, com isso será liberado memória do navegador, uma vez que foi utilizado  URL.createObjectURL(file) na linha 127 para criar uma string de URL, baseado no file, para o browser conseguir abrir o arquivo. A função é executada assim que a aplicação é fechada;

068 a 72 - Cria a função updateFile que recebe um id e data como parâmetro. Essa função será executada toda vez que o estado do UploadedFiles for alterado;

074 a 118 - Cria a função processUpload que recebe o uploadedFile como parâmetro. Essa função é responsável por processar cada arquivo que está sendo enviado pelo usuário, chamando a API e fazendo um POST com o arquivo e o nome do arquivo;

FormData representa o tipo de configuração multipart/form-data que é utilizado para enviar arquivos. É feito um append passando a chave file com o arquivo e o seu nome;







### AWS com Node.js
Em 10 passos vamos implementar uma API em Node.js que irá fazer upload de imagens em uma pasta temporária no servidor local e também no serviço S3 (Simple Storage Service) da AWS (Amazon Web Services). Iremos utilizar o MongoDB para armazenar os Posts que contém informações referente a imagem que será salva. Vamos disponibilizar as rotas para que o front end consuma a API.

Passo 1 - Criando o arquivo package.json
Crie uma pasta no seu workspace chamada backend-upload, abra no seu Editor de códigos — VsCode, e crie o arquivo package.json com a configuração abaixo:

{
  "name": "backend-upload",
  "version": "1.0.0",
  "main": "index.js",
  "license": "MIT",
  "scripts": {
    "dev": "nodemon src/index.js",
    "start": "node src/index.js"
  },
  "dependencies": {
    "aws-sdk": "^2.390.0",
    "dotenv": "^6.2.0",
    "express": "^4.16.4",
    "mongoose": "^5.4.5",
    "morgan": "^1.9.1",
    "multer": "^1.4.1",
    "multer-s3": "^2.9.0"
  },
  "devDependencies": {
    "cors": "^2.8.5",
    "nodemon": "^1.18.9"
  }
}
package.json
Dependências em produção:

aws-sdk = kit de desenvolvimento da AWS, api que utilizamos para lidar com seus serviços;
dotenv = lib que carrega as variáveis de ambiente para aplicação — arquivo .env;
express = servidor WEB que recebe requisições HTTP;
mongoose = Object Data Modeling (ODM) faz o mapeamento do Objeto (Schema) JavaScript em uma Coleção no MongoDB;
morgan = middleware que faz o log de requisições HTTP de uma maneira mais amigável para o desenvolvedor;
multer = lib que lida com upload de arquivos;
multer-s3 = lib que lida com upload de arquivos no S3/AWS.
Dependências em ambiente de desenvolvimento:

nodemon = para fazer o reload da aplicação assim que é feita uma alteração no código, exceto arquivos .env.
cors = habilita o front end consumir nosso back end (API) que estamos construindo.
scripts:

dev = vai ser utilizando apenas em desenvolvimento para o nodemon monitorar as atualizações e fazer reload do app;
start = vai ser utilizado em produção, para rodar a aplicação.
Passo 2 - Instalando as dependências
Execute um dos comandos comando abaixo:

npm install
// ou
yarn install
Após a execução do comando, a pasta node_modules que carrega todas as dependências definidas no package.json deve ficar na raiz no seu projeto.

Passo 3 - Criando a variável de ambiente
Crie o arquivo .env e .env-sample na raiz do projeto:

Ambos terão os mesmos conteúdo, porém, você vai preencher conforme as suas credenciais da Amazon que você obterá no Passo 8, por enquanto deixe assim:

.env e .env-sample:

# Se hospedar sua aplicação em algum lugar
# coloque o host aqui:
APP_URL=http://localhost:3000

# s3: para produção
# local: em desenvolvimento
STORAGE_TYPE=local

# Pode ser da sua máquina local ou Mongo Atlas
MONGO_URL=mongodb://localhost:27017/upload

# Pegue esses dados no site S3 AWS
BUCKET_NAME=
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=us-east-1
O Arquivo .env nunca deve ser enviado para o controle de versão (git), por isso existe o arquivo .env-sample que será enviado somente com as propriedades definidas, sem os valores preenchidos (a menos que os dados não sejam sensíveis).

Passo 4 - Criando o Servidor
Crie uma pasta src na raiz do projeto e dentro dela o arquivo index.js :

src/index.js:

require("dotenv").config();

const express = require("express");
const morgan = require("morgan");
const mongoose = require("mongoose");
const path = require("path");
const cors = require("cors");

const app = express();

/**
 * Database setup
 */
mongoose.connect(
  process.env.MONGO_URL,
  {
    useNewUrlParser: true
  }
);

app.use(cors());
app.use(express.json());
app.use(express.urlencoded({ extended: true }));
app.use(morgan("dev"));
app.use(
  "/files",
  express.static(path.resolve(__dirname, "..", "tmp", "uploads"))
);

app.use(require("./routes"));

app.listen(3000);
view rawindex.js hosted with ❤ by GitHub
Criando o servidor com Express no Node.js

Node.js na prática - Evento online | Rocketseat
Descubra como usar todo o potencial de Node.js criando um projeto incrível em uma aula 100% prática.

Rocketseat

1 -  Carregando para aplicação as variáveis de ambiente;

3 a 7 - Importando os arquivos necessários para criar o servidor;

9 - Criando a variável app que irá conter uma instância do servidor express;

14 a 19 - Criando a conexão com mongoose;

21 -Adicionando o middleware cors, para habilitar à API ser acessada de outra origem como um front end hospedado em outra origem;

22 - Permitindo o servidor express lidar com JSON no body da requisição.

23 - Permitindo o servidor lidar com requisições no padrão URL Encode para facilitar o envio de arquivos;

24 - Utilizando o Morgan no formato dev para fazer o logging das requisições HTTP, de maneira que o(a) dev consiga ler no terminal e entender o que está sendo requisitado — rota, parâmetros e corpo da requisição;

Exemplo:

my/user/workspace/backend-upload
POST /posts 200 1364.073 ms - 315
POST /posts 200 4152.602 ms - 272
GET /posts 200 20.996 ms - 1537
DELETE /posts/5f5bb5d24341822ebff17f2c 200 799.458 ms - -
25 a 28 - Expondo a rota files para servir arquivos estáticos, path é responsável para acessar o caminho na pasta do servidor, __dirname  é o diretório onde o path está sendo executado;

30 - Importa o arquivo de rotas que vamos criar logo em seguida e utiliza como um middleware que recebe as requisições;

32 - Inicia o servidor e disponibiliza a aplicação na porta 3000.

Passo 5 -  Criando as Rotas da aplicação
Crie o arquivo routes.js dentro da pasta src:

src/routes.js

const routes = require("express").Router();
const multer = require("multer");
const multerConfig = require("./config/multer");

const Post = require("./models/Post");

routes.get("/posts", async (req, res) => {
  const posts = await Post.find();

  return res.json(posts);
});

routes.post("/posts", multer(multerConfig).single("file"), async (req, res) => {
  const { originalname: name, size, key, location: url = "" } = req.file;

  const post = await Post.create({
    name,
    size,
    key,
    url
  });

  return res.json(post);
});

routes.delete("/posts/:id", async (req, res) => {
  const post = await Post.findById(req.params.id);

  await post.remove();

  return res.send();
});

module.exports = routes;
view rawroutes.js hosted with ❤ by GitHub
1 - Importa o roteador do express — Router. E atribui na constante router.

2 - Importa o multer que lida com upload de arquivos;

3 - Importa a configuração do multer que iremos criar em seguida;

5 - Importa o model Post que é a representação de um Post do Objeto JavaScript para o mongoDB. Vamos criar o model Post em seguida;

7 a 10 -  Criamos uma rota /post que recebe as requisições GET que irá buscar todos os posts incluídos na base de dados do mongodb na coleção Post e retorna via JSON um array de posts.

13 a 24 -  Criamos uma rota /post que recebe as requisições POST, ela irá receber o arquivo, usando o multer com as configurações. Irá receber um arquivo por vez (single) da requisição no parâmetro file. Será pego os dados da imagem quem vem no atributo file: nome, tamanho do arquivo, nome do arquivo (key) e a URL, com esses dados em mãos iremos criar um Post no banco de dados. Por fim será retornado o JSON com os dados do Post.

26 a 32 - Criamos uma rota /post/:id que que recebe requisições DELETE com um parâmetro id informado na rota. Buscamos o Post pelo ID, removemos usando o await post.remove() e retornamos um status 200.

34 - exportamos esse módulo de rotas que foi importado no arquivo index.js.

Passo 6 - Configurando o Multer para salvar imagem no disco e no S3
Crie a pasta config dentro da pasta src. Nela irá conter o arquivo multer.js com as configurações para salvar imagens na pasta temporária: tmp/uploads e também no bucket do S3.

src/config/multer.js

const multer = require("multer");
const path = require("path");
const crypto = require("crypto");
const aws = require("aws-sdk");
const multerS3 = require("multer-s3");

const MAX_SIZE_TWO_MEGABYTES = 2 * 1024 * 1024;

const storageTypes = {
  local: multer.diskStorage({
    destination: (req, file, cb) => {
      cb(null, path.resolve(__dirname, "..", "..", "tmp", "uploads"));
    },
    filename: (req, file, cb) => {
      crypto.randomBytes(16, (err, hash) => {
        if (err) cb(err);

        file.key = `${hash.toString("hex")}-${file.originalname}`;

        cb(null, file.key);
      });
    },
  }),
  s3: multerS3({
    s3: new aws.S3(),
    bucket: process.env.BUCKET_NAME,
    contentType: multerS3.AUTO_CONTENT_TYPE,
    acl: "public-read",
    key: (req, file, cb) => {
      crypto.randomBytes(16, (err, hash) => {
        if (err) cb(err);

        const fileName = `${hash.toString("hex")}-${file.originalname}`;

        cb(null, fileName);
      });
    },
  }),
};

module.exports = {
  dest: path.resolve(__dirname, "..", "..", "tmp", "uploads"),
  storage: storageTypes[process.env.STORAGE_TYPE],
  limits: {
    fileSize: MAX_SIZE_TWO_MEGABYTES,
  },
  fileFilter: (req, file, cb) => {
    const allowedMimes = [
      "image/jpeg",
      "image/pjpeg",
      "image/png",
      "image/gif",
    ];

    if (allowedMimes.includes(file.mimetype)) {
      cb(null, true);
    } else {
      cb(new Error("Invalid file type."));
    }
  },
};
view rawmulter.js hosted with ❤ by GitHub
1 a 5 - Importamos os módulos necessários para lidar com os arquivos enviados na rota /posts via método POST. Tanto os arquivos que serão salvos no servidor local quanto no servidor no S3 da AWS.

7 - Definimos a constante que armazena o valor máximo (2 MB) permitido para uploads de arquivo, abstraindo a conta matemática que converte 2 Megabytes em um valor inteiro, resolvemos o problema de números mágicos, seguindo uma boa prática do Clean Code 😀

9 a 39 - Criamos um objeto storageTypes com duas propriedades: local e s3.

Na propriedade local, utilizamos o multer para para salvar no disco (servidor local) usando a função diskStorage que recebe a propriedade destination que recebe uma função com os três parâmetros (req, file, callback) chamamos o cb passando null para o erro, e o caminho de onde vai ser salvo o arquivo, nesse caso em uma pasta tmp/uploads na raiz do projeto.

A propriedade filename é uma função que recebe os mesmos parâmetros da função anterior, implementamos uma lógica para gerar o nome do arquivo usando um hash para representar o nome do arquivo mais o nome original da imagem. No final é chamada a função cb com dois parâmetros, o erro é null e o segundo é o nome do arquivo: file.key.

Já na propriedade s3 é feita a configuração para salvar os dados no serviço S3. Usando a função multerS3 passamos as configurações:

s3 = recebe uma instância do aws.S3
bucket = nome do bucket que criamos no site da S3;
contentType = serve para abrir a imagem no navegador ao invés de forçar o download;
acl = são as permissões, public-read significa que nossa API pode ter acesso ao bucket;
key = nome da imagem.
41 a 61 - exportamos o módulo multerConfig passando as propriedades:

dest = caminho para a pasta uploads  onde são salvos arquivos temporariamente;
storage = onde serão salvos os arquivos, pode ser local ou s3, depende do que foi configurado na variável de ambiente STORAGE_TYPE em ambiente de dev: local e ambiente de produção s3;
limits recebe o objeto fileSize com o valor inteiro do tamanho máximo permitido para uploads de arquivo;
fileFilter função que filtra os tipos de arquivos que serão aceitos, se o arquivo enviado não estiver incluído no array de arquivos permitidos é lançado um erro para o usuário caso contrário é permitido e continua a operação.
Passo 7 - Criando o Model Post
Dentro de src crie a pasta models com arquivo Post.js

PostSchema será a entidade que representará um Post tanto no Objeto JavaScript quando na coleção do MongoDB. O Mongoose irá fazer essa intermediação, mapeando a relação Objeto ↔  Documento e fornecendo interfaces para um CRUD completo.

src/models/Post.js

const mongoose = require("mongoose");
const aws = require("aws-sdk");
const fs = require("fs");
const path = require("path");
const { promisify } = require("util");

const s3 = new aws.S3();

const PostSchema = new mongoose.Schema({
  name: String,
  size: Number,
  key: String,
  url: String,
  createdAt: {
    type: Date,
    default: Date.now,
  },
});

PostSchema.pre("save", function () {
  if (!this.url) {
    this.url = `${process.env.APP_URL}/files/${this.key}`;
  }
});

PostSchema.pre("remove", function () {
  if (process.env.STORAGE_TYPE === "s3") {
    return s3
      .deleteObject({
        Bucket: process.env.BUCKET_NAME,
        Key: this.key,
      })
      .promise()
      .then((response) => {
        console.log(response.status);
      })
      .catch((response) => {
        console.log(response.status);
      });
  } else {
    return promisify(fs.unlink)(
      path.resolve(__dirname, "..", "..", "tmp", "uploads", this.key)
    );
  }
});

module.exports = mongoose.model("Post", PostSchema);
view rawpost.js hosted with ❤ by GitHub
1 a 5 - Importamos as bibliotecas necessárias para criar o Schema Post usando mongoose, e a outras bibliotecas que irão lidar com o arquivo para gerar um link completo e deletar as imagens.

7 - Criamos uma constante s3 que recebe uma instância da biblioteca S3 da AWS;

9 a 18 - Definimos o Schema do Post, com os atributos necessários com seus respectivos tipos de dados. Mongoose (ODM) vai fazer com que esse objeto seja compatível com a MongoDB.

20 a 24 - Criamos um lógica que antes (pre) que for salvo algum documento no MongoDB essa função será chamada. Ela basicamente utiliza o this referente ao PostSchema para adicionar na url o endereço do servidor representado pela variável de ambiente APP_URL mais /files/ e o nome do arquivo que está na variável this.key:

Representação:

http://localhost:3000/files/c8a934791778f64650c57dd3c94d8d47-minhafoto.png
26 a 45 - Criamos um lógica antes (pre) que for chamada alguma função de deleção de documentos no MongoDB, a função seja executada.

Se estiver no ambiente STORAGE_TYPE = "s3" a lógica do if é executada, deletando do bucket definido no BUCKET_NAME o arquivo (key) this.key.

Se não estiver no ambiente da S3 então é removido o arquivo do servidor local, usando o file system (fs) do Node.js que vai fazer unlink para remover o arquivo. É utilizado o promisify do Node.js para deixar o código em formato de promises tornando mais elegante e não sendo necessário lidar com callbacks. Para dentro da promise do unlink vai o caminho resolvido via path.resolve do arquivo no servidor.

Passo 8 - Criando um Bucket no S3 da AWS
Deixei os vídeos no momento exato onde começa a falar sobre assunto:

Crie um Bucket seguindo os mesmos passos do vídeo.
https://www.youtube.com/watch?v=MkkbUfcZUZM&t=1923s

Depois crie um usuário no Identity and Access Management (IAM) da AWS.
https://www.youtube.com/watch?v=MkkbUfcZUZM&t=2058s

Dê permissão ao acesso público do bucket (ACL):
https://www.youtube.com/watch?v=MkkbUfcZUZM&t=2701s

Pronto, agora já podemos continuar.

Passo 9 - Iniciando o MongoDB e conferindo as variáveis de ambiente
Antes de iniciar o App, você precisa estar com o MongoDB rodando na máquina, utilize o Docker ou MongoAltas.

Se você não tiver o MongoDB no seu Docker, crie um container usando esse comando:

docker run --name mongo -p 27017:27017 -d -t mongo
Confira se o mongo já está executando:

docker ps
Para saber se o mongo está funcionando, acesse a URL: http://localhost:27017/

Resultado esperado:

It looks like you are trying to access MongoDB over HTTP on the native driver port.
Utilizando o MongoDB Compass ou Robo 3T,  crie um banco de dados chamado upload e uma coleção Post.

Por fim verifique se as variáveis de ambiente estão preenchidas:

.env:

# Se hospedar sua aplicação em algum lugar
# coloque o host aqui:
APP_URL=http://localhost:3000

# s3 para produção
# local em desenvolvimento
STORAGE_TYPE=s3

# Pode ser da sua máquina local ou Mongo Atlas
MONGO_URL=mongodb://localhost:27017/upload

# Pegue esses dados no site S3 AWS
BUCKET_NAME=tutorialuploadfile
AWS_ACCESS_KEY_ID=123JH12K3H1KJ3K1
AWS_SECRET_ACCESS_KEY=123JK12H3JK1+23232321AASD+ggn4qbkgyCI
AWS_DEFAULT_REGION=us-east-1
Se for testar no S3 mantenha o STORAGE_TYPE=s3, senão, deixe STORAGE_TYPE=local

Recomendo testar primeiro localmente.

Passo 10 - Iniciando o servidor e fazendo requisições com Insomnia
Para iniciar a aplicação basta executar o comando:

yarn dev
// ou
npm dev
Abra o Insomnia e crie três rotas:

POST http://localhost:3000/posts
GET http://localhost:3000/posts
DELETE http://localhost:3000/posts/5f5bb5d24341822ebff17f2c
Tente criar, buscar e deletar o Post.

Teste fazer o upload tanto na máquina local quando no S3.

Criando um Post na rota posts com o método POST

Listando os Posts na rota posts com o método GET

Deletando um post pelo seu ID na rota posts com o método DELETE

Qualquer dúvida pergunte aqui nos comentários ou na comunidade do Discord!

👍 Conclusão
Com poucos arquivos e poucas linhas de código, conseguimos criar um servidor web, expor três rotas para listar, deletar e criar posts. Fazer upload de imagens tanto em disco local quanto no S3 da AWS.

Se ficou alguma dúvida, o Diego Fernandes fez um vídeo explicando como fazer upload de imagens no back end Node.js, confere lá:

https://www.youtube.com/watch?v=MkkbUfcZUZM&t=7s

### React Native
