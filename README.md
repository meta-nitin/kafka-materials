# kafka-materials

// Producer

1. Properties props = new Properties();
   props.setProperty(ProducerConfig.BOOTSTRAP_SERVER_CONFIG, "abc");
   props.setProperty(ProducerConfig.KEY_SERIALIZER, StringSerializer.class);
   props.setProperty(ProducerConfig.VALUE_SERIALIZER, StringSerializer.class);

2. KafkaProducer<String, String> producer = new KafkaProducer<>(props);

3. ProducerRecord<String, String> producerRecord = new ProducerRecord<>(topic,key,value);

4. producer.send(producerRecord, new CallBack(){
	   void onCompletion(RecordMetaData metadata) {
		  log.info("Successfully written in topic");
		  }
	   })
	


// Consumer

1. Properties props = new Properties();
   props.setProperty(ConsumerConfig.BOOTSTRAP_SERVER_CONFIG, "abc");
   props.setProperty(ConsumerConfig.KEY_DESERIALIZER, StringDeserializer.class);
   props.setProperty(ConsumerConfig.VALUE_DESERIALIZER, StringDeserializer.class);
   
2. KafkaConsumer<String, String> consumer = new KafkaConsumer<>(props);

3. consumer.subscribe(Arrays.asList("topicA", "topicB"));

4. //poll
   ConsumerRecords<String, String> consumerRecords = null;
   do{
	  consumerRecords = consumer.poll(1000); // poll and immediately return results or wait till timeout
	  if(null!= consumerRecords && !consumerRecords.isEmpty()) {
		  for (ConsumerRecord<Object, Object> record : consumerRecords) {
			  log.info(record.key() + record.value());
			  }
		  }
	} while(null != records && !records.isEmpty())
