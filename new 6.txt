package FirstEclipse.example.FirstEclipse;

import org.apache.logging.log4j.LogManager;


import org.apache.logging.log4j.Logger;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Import;
import org.springframework.context.annotation.Primary;
import org.springframework.context.annotation.PropertySource;
import org.springframework.context.support.PropertySourcesPlaceholderConfigurer;

import FirstEclipse.example.FirstEclipse.util.propertyFile;



@Configuration
@ComponentScan
@PropertySource(value = { "classpath:application.properties",
		"classpath:queries.properties", "classpath:messages.properties"})
@Import({DBConfig.class})

public class AppConfig 
{

	private static final Logger logger = LogManager.getLogger(AppConfig.class);
    
    @Bean
    public static PropertySourcesPlaceholderConfigurer placeHolderConfigurer()
    {
        return new PropertySourcesPlaceholderConfigurer();
    }  
    
 
    
    @Bean
    @Qualifier("application")
    @Primary
    public propertyFile propertyFileReaderApplication() {
        	return new propertyFile("application");
    }
   
    @Bean("queries")
    @Qualifier("queries")
    public propertyFile propertyFileReaderQueries() {
        	return new propertyFile("queries");
    }
    
    @Bean("messages")
    @Qualifier("messages")
    public propertyFile propertyFileReaderMessages() {
        	return new propertyFile("messages");
    }
    
   /* @Bean("constants")
    @Qualifier("constants")
    public propertyFile propertyFileReaderConstants() {
    	return new propertyFile("constants");
}*/
    
}
