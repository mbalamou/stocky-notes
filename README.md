## Stocky notes

### How to update rest-api version
1. Look for breaking changes in the [release notes](https://shopify.dev/api/release-notes/) in the **Rest API section**
	- Example of a breaking change in [2021-10](https://shopify.dev/api/release-notes/)
2. Handle the breaking changes (this will be case by case and cannot be generalized here)
3. Update `config.api_version` in this file `config/initializers/shopify_app.rb` 
	```ruby
		config.api_version = "2021-10"
	```
4. Run `dev test`
5. The output might have the following messages:

```txt
	  VCR is currently using the following cassette:
              - /Users/michelbalamou/src/github.com/Shopify/stocky/spec/fixtures/api_responses/Sync_Shopify_AverageCostJob/_perform/updates_inventory_item_cost_to_be_variant_average_cost.yml
```

6. Proceed to find all the `yaml` files in the output and delete them, then re-run `dev test`. This will regenerate the `yaml` files.
7. After regenerating all the `yaml` files the output might still have errors, but they should be unrelated to the `yaml` files. Proceed to handle them (again this will be different for each breaking change).
