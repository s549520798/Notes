## Spring Boot 实现分页查询
1. 创建实体类
````
@EntityListeners(AuditingEntityListener.class)
@Entity
public class Article {
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;
    @Column(name = "title")
    private String title;           //帖子 标题
    @Column(name = "content")
    private String content;         //帖子 内容
    @CreatedDate
    @Column(name = "post_time")
    private Date postTime;        //发布时间
    // .... getter and setter 省略

````
2. 实现Repository,定义ArticleRepository接口 继承自PagingAndSortingRepository
````
public interface ArticleRepository extends ,PagingAndSortingRepository<Article,Long>{
}

````
3. 创建Contorller类
````
@RestController
@RequestMapping(value = "/article")
public class ArticleController {
    private final ArticleRepository repository;
    private static final Logger log = LoggerFactory.getLogger(ArticleController.class);

    @Autowired
    public PostController(ArticleRepository repository) {
        this.repository = repository;
    }

    @GetMapping(value = "/{page}/article")
    public List<Post>> getArticles(@PathVariable int page){
        int pageSize = 10;
        //注意： "postTime" 是数据库在实体类中映射的字段
        Sort sort = Sort.by(new Sort.Order(Sort.Direction.DESC,"postTime"));
        PageRequest pageRequest =  PageRequest.of(page,pageSize,sort);
        Page<Article> articlePage = repository.findAll(pageRequest);
        log.info("一共有的article的数目 ======" + articlePage.getTotalElements());
        log.info("一共分了多少页 =====" + articlePage.getTotalPages());
        log.info("当前页面所有数 =====" + articlePage.getContent().size());
        return articlePage.getContent();
    }
````
> 注意："postTime" 是数据库在实体类中映射的字段