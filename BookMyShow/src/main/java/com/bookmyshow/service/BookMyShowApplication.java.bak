package com.bookmyshow.service;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.hystrix.EnableHystrix;
import org.springframework.context.annotation.Bean;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.client.RestTemplate;

import com.netflix.hystrix.contrib.javanica.annotation.HystrixCommand;



@SpringBootApplication
@RestController
@EnableHystrix
@RequestMapping("/bookmyshow")
public class BookMyShowApplication {
	@Autowired
	private  RestTemplate template;
	
	@GetMapping("/bookTicket")
	public String bookShow()
	{
		String paytmService=template.getForObject("http://localhost:8081/paytm/pay",String.class);
		String notifyService=template.getForObject("http://localhost:8082/notificationservice/notify",String.class);
		return  "Called Service"+paytmService+":"+notifyService;
	}

	@GetMapping("/bookTicketWithHytrix")
	@HystrixCommand(commandKey="book key",groupKey="bookshow",fallbackMethod="bookShowFallBack")
	public String bookShowWithHytrix()
	{
		String paytmService=template.getForObject("http://localhost:8081/paytm/pay",String.class);
		String notifyService=template.getForObject("http://localhost:8082/notificationservice/notify",String.class);
		return  "Called Service"+paytmService+":"+notifyService;
	}
	
	public static void main(String[] args) {
		SpringApplication.run(BookMyShowApplication.class, args);
	}
	

	public String bookShowFallBack()
	{
	
		String paytmService=template.getForObject("http://localhost:8081/paytm/pay2",String.class);
		return "Servic getway failed";
	}
	
	
	@Bean
	public RestTemplate template()
	{
		return new RestTemplate();
	}
 
}
