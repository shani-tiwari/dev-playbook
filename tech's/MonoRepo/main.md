# MonoRepo 
- Management tool to provide shared code/feature/ui across different projects/apps.
- shared code sitn in 'packages'
- 'apps' contain all of your apps/projects

## featuers: (provided by tools)
- Task Ordering
- Caching
- Parallelism
- inc CI

- Tools:
  - turborepo -- popular, open-source, free -- by vercel 
  - Nx -- open-source, paid -- by Nrwl  
  - Bit -- open-source, versionless, cloud-hosted 

- Scenrio:
  - 4 different repo's -- each one have different tech stack, different CI/CD pipeline, different team, different deployment pipeline, different folder structure but have a same feature across all(code repeats in every project)
  - Suppose u have to make an feature/app and that feature can be used in other projects too, so u can create an package and reuse it in other projects -- makes it easy to maintain and update

  
