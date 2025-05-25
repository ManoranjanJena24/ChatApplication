# React + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh

## Expanding the ESLint configuration

If you are developing a production application, we recommend using TypeScript with type-aware lint rules enabled. Check out the [TS template](https://github.com/vitejs/vite/tree/main/packages/create-vite/template-react-ts) for information on how to integrate TypeScript and [`typescript-eslint`](https://typescript-eslint.io) in your project.









---------------------------------------------------------------------------------------------------------------------------------------------------------------


FRONTEND STARTING HERE

npm create vite@latest my-react-app -- --template react



-> npm i react-router-dom react-hot-toast



#### tailwind installation part given below

step 1) paste this code:  npm install tailwindcss @tailwindcss/vite




after this first command if you check the package.json u will see in dependecies  @tailwindcss/vite": "^4.1.7",


step2) for step 2 we have to navigate to the vite.config.ts file and add this 2 lines there(marked in blue)

import { defineConfig } from 'vite'
## import tailwindcss from '@tailwindcss/vite'
export default defineConfig({
  plugins: [
   ## tailwindcss(),
  ],
})





##### original one i will se 

import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import tailwindcss from '@tailwindcss/vite'

// https://vite.dev/config/
export default defineConfig({
  plugins: [
    tailwindcss(),
    react()
  
  ],
})



step3) inside src folder we go index.css and add the the code  at the top


@import "tailwindcss";






