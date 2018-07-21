# gombda
## overview
This Library is  thin rapper for Easier to use api gateway and lambda.

## example

    func (h handler) Router(request events.APIGatewayProxyRequest) (events.APIGatewayProxyResponse, error) {
	g := gombda.New(request)
	g.POST("/", h.Create)
	g.GET("/{id}", h.Show)
	g.DELETE("/{id}", h.Destroy)
	g.PATCH("/{id}", h.Update)
	g.GET("/", h.Index)

	return g.Start()
    }
    
    func (h handler) Create(request events.APIGatewayProxyRequest) (events.APIGatewayProxyResponse, error) {
    	// jsonの値を取得
    	title := gjson.Get(request.Body, "title").String()
    	h.dynamoModel.Create(title)
    
    	return events.APIGatewayProxyResponse{
    		Body:       fmt.Sprintf("success\n"),
    		StatusCode: 200,
    		Headers: map[string]string{
    			"Access-Control-Allow-Origin":      "*",
    			"Access-Control-Allow-Credentials": "true",
    		},
    	}, nil
    }
