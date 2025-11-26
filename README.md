# Boutique Diayma

## Traçage avant l’affichage des produits (accueil)

Mode utilisé: Pas à pas détaillé (F11).

### Points d’arrêt (emplacements demandés)
- Components/CartSummaryViewComponent.cs — ligne 12
- Controllers/ProductController.cs — ligne 15
- Controllers/OrderController.cs — ligne 17
- Controllers/CartController.cs — ligne 15
- Startup.cs — ligne 20

### Chemin d’exécution — Pas à pas détaillé
1) Namespace: P2FixAnAppDotNetCode
   - Classe: Startup
   - Méthode: Startup(IConfiguration configuration)
   - Action: construction de Startup
   - Mode: Pas à pas détaillé

2) Namespace: P2FixAnAppDotNetCode
   - Classe: Startup
   - Méthode: ConfigureServices(IServiceCollection services)
   - Actions clés: enregistrement DI et MVC
     - AddLocalization
     - AddSingleton<ICart, Cart>
     - AddSingleton<ILanguageService, LanguageService>
     - AddTransient<IProductService, ProductService>
     - AddSingleton<IProductRepository, ProductRepository>
     - AddTransient<IOrderService, OrderService>
     - AddTransient<IOrderRepository, OrderRepository>
     - AddMvc().AddViewLocalization().AddDataAnnotationsLocalization()
     - Configure<RequestLocalizationOptions>
   - Mode: Pas à pas détaillé

3) Namespace: P2FixAnAppDotNetCode
   - Classe: Startup
   - Méthode: Configure(IApplicationBuilder app, IHostingEnvironment env)
   - Actions clés: pipeline HTTP
     - UseStaticFiles
     - UseRequestLocalization
     - UseSession
     - UseMvc (route par défaut {controller=Product}/{action=Index})
   - Mode: Pas à pas détaillé

4) Requête HTTP GET "/" (navigateur)
   - Résolution de route → controller par défaut Product / action Index
   - Mode: Pas à pas détaillé

5) Namespace: P2FixAnAppDotNetCode.Controllers
   - Classe: ProductController
   - Méthode: ProductController(IProductService, ILanguageService)
   - Action: injection des dépendances via le conteneur
   - (Breakpoint ligne 15 atteint)
   - Mode: Pas à pas détaillé

6) Namespace: P2FixAnAppDotNetCode.Controllers
   - Classe: ProductController
   - Méthode: IActionResult Index()
   - Action: appel du service produits → _productService.GetAllProducts()
   - Mode: Pas à pas détaillé

7) Namespace: P2FixAnAppDotNetCode.Models.Services
   - Classe: ProductService
   - Méthode: List<Product> GetAllProducts()
   - Action: délègue au repository → _productRepository.GetAllProducts()
   - Mode: Pas à pas détaillé

8) Namespace: P2FixAnAppDotNetCode.Models.Repositories
   - Classe: ProductRepository
   - Méthode: Product[] GetAllProducts()
   - Action: filtre par Stock > 0, trie par Name, retourne le tableau
   - Mode: Pas à pas détaillé 

### Résumé des éléments visités (avant affichage produits)
- Namespaces clés: 
  - P2FixAnAppDotNetCode (Startup)
  - P2FixAnAppDotNetCode.Controllers (ProductController)
  - P2FixAnAppDotNetCode.Models.Services (ProductService)
  - P2FixAnAppDotNetCode.Models.Repositories (ProductRepository)
  - P2FixAnAppDotNetCode.Components (CartSummaryViewComponent)
- Classes/Méthodes: 
  - Startup.Startup → Startup.ConfigureServices → Startup.Configure
  - ProductController.ProductController → ProductController.Index
  - ProductService.GetAllProducts
  - ProductRepository.GetAllProducts
  - CartSummaryViewComponent.(ctor) → Invoke
