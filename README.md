Elasticsearch Quartz
=======================

## Overview

Elasticsearch Quartz Plugin is a scheduler for Elasticsearch plugins.
In your Elasticsarch plugin, you can register a job and start it at a specified time.

## Installation

### Install Quartz Plugin

    $ $ES_HOME/bin/plugin -install org.codelibs/elasticsearch-quartz/1.0.1

## Usage

### Edit pom.xml

To use ScheduleService, put the following dependency to your pom.xml.

    <dependency>
      <groupId>org.codelibs</groupId>
      <artifactId>elasticsearch-quartz</artifactId>
      <version>1.0.1</version>
      <scope>provided</scope>
    </dependency>

### Inject ScheduleService

Quartz plugin provides ScheduleService instance to DI container(Guice) of Elasticsearch.
Therefore, you can use scheduleService in your Service or River class as below:

    @Inject
    public YourRiver(final RiverName riverName, final RiverSettings settings,
        final Client client, final ScheduleService scheduleService) {
        ...

ScheduleService delegates Scheduler's methods of Quartz.

### Register Job

ScheduleService allows you to register your Job and Trigger of Quartz.

    scheduleService.scheduleJob(job, trigger);

### Unregister Job

You can remove your job by group and job ID.

    import static org.quartz.JobKey.jobKey;
    
    ...
    
    scheduleService.deleteJob(jobKey(jobId, groupId));



