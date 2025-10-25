# Tutorial Tailwind CSS

Tutorial to configure:  
Tailwind CSS + Automatic Class Sorting

- IMPORTANTE !

    Esse tutorial é uma continuação da configuração do front-end usando React com TypeScript usando o Vite.  
     Antes deve ser concluído esse outro tutorial, para instalando e configurando o Vite, Prettier, etc:  
     [Tutorial React + Code Format](https://github.com/rramires/fe1_react_code-format/blob/master/README.md)

    Seguido do tutorial para instalação do React Router DOM:  
     [Tutorial React + React Router DOM](https://github.com/rramires/fe2_react-router-dom/blob/master/README.md)

---

1 - Instale o Tailwind CSS:  
[Tailwind CSS Using Vite](https://tailwindcss.com/docs/installation/using-vite)

```sh
pnpm add tailwindcss @tailwindcss/vite
```

2 - Caso não tenha ainda, instale a extensão do Tailwind no VSCode:  
[Tailwind CSS IntelliSense](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss)

3 - Atualize o **vite.config.ts**, adicionando:

```js
// adicione
import tailwindcss from '@tailwindcss/vite'

// em plugins adicione
/* plugins: [react()*/ , tailwindcss() /*],*/
```

4 - Crie um arquivo **global.css** dentro de **src** e adicione:

```css
@import 'tailwindcss';
```

5 - Importe **global.css** no **main.tsx**:

```js
// adicione
import './global.css'
```

6 - Rode a aplicação:

```sh
pnpm dev
```

- Acessando via http://localhost:3001 perceba que a formatação padrão do html sumiu, deixando as fontes pequenas.

7 - Comite como:

```sh
git add .
git commit -m "feat: add Tailwind CSS integration with configuration and global styles"
git push
```

---

1 - Instale o plugin para organizar a ordem das classes no Tailwind:  
[Automatic Class Sorting](https://tailwindcss.com/blog/automatic-class-sorting-with-prettier)

```sh
pnpm add -D prettier-plugin-tailwindcss
```

2 - Adicione no arquivo de configuração do Prettier, **.prettierrc.json**:

```js
// depois de
/* "arrowParens": "always" */,
"plugins": ["prettier-plugin-tailwindcss"]
```

3 - Para testar, adicione alguns estilos no return do nosso layout em **\_layouts/app-layout.tsx**:

```js
<div className='flex h-screen flex-col'>
	<header className='flex h-20 items-center bg-slate-800 pl-8 text-slate-200'>
		<h1 className='text-3xl font-bold'>AppLayout Header</h1>
	</header>
	<main className='flex flex-1'>
		{/* Content will change here */}
		<Outlet />
	</main>
	<footer className='flex h-12 items-center bg-slate-800 pl-8 text-slate-200'>
		<p>AppLayout Footer</p>
	</footer>
</div>
```

4 - Adicione alguns estilos na nossa página Home em **pages/app/home.tsx**:

```js
<>
	<PageTitle title='Home' />
	<div className='flex-1 bg-slate-900 px-8 py-4 text-slate-100'>
		<h2 className='text-2xl font-medium'>Home Page!</h2>
	</div>
</>
```

- Perceba o autocomplete funcionando dentro do className, graças a extensão instalada no passo 3.

- Veja tamtém a ordem classificação das classes, invertendo a ordem
  **' font-medium text-2xl'** e vendo que volta para **'text-2xl font-medium'** quando salva, graças ao prettier-plugin-tailwindcss.

5 - Adicione também alguns estilos no return do nosso layout em **\_layouts/unauth-layout.tsx**:

```js
<div className='flex h-screen flex-col'>
	<header className='flex h-8 items-center bg-slate-800 pl-8 text-slate-200'></header>
	<main className='flex flex-1'>
		{/* Content will change here */}
		<Outlet />
	</main>
	<footer className='flex h-8 items-center bg-slate-800 pl-8 text-slate-200'></footer>
</div>
```

6 - Adicione também um form de login de exemplo na página SignIn:

```js
// Dentro do SignIn()
const handleSubmit = (e: React.SubmitEvent<HTMLFormElement>) => {
	e.preventDefault()
	// Add login logic here
}
```

e

```js
// No return
<>
	<PageTitle title='Sign In' />
	<div className='flex flex-1 items-center justify-center bg-slate-900 px-8 py-4 text-slate-100'>
		<div className='w-full max-w-md rounded-lg bg-slate-800 p-8 shadow-lg'>
			<h2 className='mb-6 text-center text-2xl font-medium'>Login</h2>

			<form onSubmit={handleSubmit} className='space-y-4'>
				<div>
					<label
						htmlFor='username'
						className='mb-1 block text-sm font-medium'
					>
						Username
					</label>
					<input
						id='username'
						type='text'
						placeholder='Enter your username'
						className='w-full rounded-md border border-slate-600 bg-slate-700 px-4 py-2 text-slate-100 placeholder-slate-400 focus:border-slate-500 focus:ring-1 focus:ring-slate-500 focus:outline-none'
						required
					/>
				</div>

				<div>
					<label
						htmlFor='password'
						className='mb-1 block text-sm font-medium'
					>
						Password
					</label>
					<input
						id='password'
						type='password'
						placeholder='Enter your password'
						className='w-full rounded-md border border-slate-600 bg-slate-700 px-4 py-2 text-slate-100 placeholder-slate-400 focus:border-slate-500 focus:ring-1 focus:ring-slate-500 focus:outline-none'
						required
					/>
				</div>

				<button
					type='submit'
					/* disabled */
					className='mt-6 w-full rounded-md bg-blue-900 px-4 py-2 font-semibold text-white transition-colors enabled:cursor-pointer enabled:hover:bg-blue-800 disabled:cursor-not-allowed disabled:opacity-60'
				>
					Login
				</button>
			</form>
		</div>
	</div>
</>
```

7 - Rode para verificar:

```sh
pnpm dev
```

- Veja o conteúdo das páginas Home e SignIn, centralizados e com os h2 formatados.

8 - Vamos adicionar alguma formatação nas páginas de erro, **e404.tsx** e **error.tsx**, que ficarão assim, respectivamente:

```js
<>
	<PageTitle title='Not Found' />
	<div className='flex h-screen flex-col items-center justify-center bg-slate-900 p-8 text-slate-100'>
		<h1 className='text-3xl font-bold'>404 - Page not found</h1>
		<h3 className='pt-3 font-bold text-slate-500'>
			<a
				className='hover: :hover:text-slate-100 ml-1 hover:underline'
				href='/'
			>
				Return to homepage
			</a>
		</h3>
	</div>
</>
```

```js
<>
	<PageTitle title='Error' />
	<div
		id='error-page'
		className='flex h-screen flex-col items-center justify-center bg-slate-900 p-8 text-slate-100'
	>
		<h1 className='text-3xl font-bold'>Oops!</h1>
		<p className='pt-1'>Sorry, an error occurred:</p>
		<p className='pt-3'>
			<i className='text-red-600'>{error.statusText || error.message}</i>
		</p>
	</div>
</>
```

- Lembrando que para testar essas páginas de erro devemos:  
  Usar uma rota inexistente **http://localhost:3001/other** para ver o **e404.tsx** sendo renderizado.

    Provocar um erro em alguma página, adicionando por exemplo na Home: **throw new Error('Home error simulation')**, e ir para **http://localhost:3001/**, para ver o **error.tsx** sendo renderizado.

9 - Comite como:

```sh
git add .
git commit -m "feat: add Tailwind CSS styles and integrate prettier-plugin-tailwindcss for class sorting"
git push
```
