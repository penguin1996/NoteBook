```java
/**
 * @author zero
 * {@code @Date} 15:18 2023/12/26
 * {@code @Description} 风控评级处理类
 **/
@RestController
@Slf4j
@RequestMapping("api/admin/cdd/")
@Tag(name = "CddRiskRatingController", description = "cdd风控评级处理")
public class CddRiskRatingController {

    @Resource
    CddRiskRatingService cddRiskRatingService;

    @NoAuth(NoAuth.INTERNAL)
    @PostMapping("/saveCddRiskRating")
    @Operation(summary = "保存风控评级数据+风控评级计算")
    public Result saveCddRiskRating(@Valid @RequestBody() CddRiskRatingDTO cddRiskRatingDTO) {
        return Result.ok(cddRiskRatingService.saveCddRiskRating(cddRiskRatingDTO));
    }
}
```

