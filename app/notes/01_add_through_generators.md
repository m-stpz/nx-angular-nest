# Add through generators

- Since we're using `nx`, we add everything through generators, instead of manually

### NestJS generators

```bash
pnpm nx g @nx/nest:module <path>
# to nest, we can do
# path = `./apps/api/src/users/users`

pnpm nx g @nx/nest:module ./apps/api/src/users/users # module
pnpm nx g @nx/nest:controller <path> # controller
pnpm nx g @nx/nest:service <path> # controller
```
