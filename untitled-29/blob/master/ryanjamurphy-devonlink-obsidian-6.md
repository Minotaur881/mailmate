# ryanjamurphy/DEVONlink-obsidian

[Permalink](https://github.com/ryanjamurphy/DEVONlink-obsidian/blob/96acf02beebb47591f9d6e65ddff5dae0febfa43/rollup.config.js)

Cannot retrieve contributors at this time

|  | import typescript from '@rollup/plugin-typescript'; |
| :--- | :--- |
|  | import {nodeResolve} from '@rollup/plugin-node-resolve'; |
|  | import commonjs from '@rollup/plugin-commonjs'; |
|  |  |
|  | const banner = |
|  | \`/\* |
|  | THIS IS A GENERATED/BUNDLED FILE BY ROLLUP |
|  | if you want to view the source visit the plugins github repository |
|  | \*/ |
|  | \`; |
|  |  |
|  | export default { |
|  |  input: 'main.ts', |
|  |  output: { |
|  |  dir: '.', |
|  |  sourcemap: 'inline', |
|  |  format: 'cjs', |
|  |  exports: 'default', |
|  |  banner, |
|  |  }, |
|  |  external: \['obsidian'\], |
|  |  plugins: \[ |
|  |  typescript\(\), |
|  |  nodeResolve\({browser: true}\), |
|  |  commonjs\(\), |
|  |  \] |
|  | }; |

