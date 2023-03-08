---
title: AWS Transcribe: Automating Speech-to-Text Transcription in the Cloud
description: 
published: true
date: 2023-02-19T03:32:24.075Z
tags: 
editor: markdown
dateCreated: 2023-02-19T03:32:22.715Z
---

- [AWS Transcribe: 클라우드에서 음성-텍스트 변환 자동화***Korean** document is available*](/ko/Knowledge-base/Cloud/aws-transcribe-automating-speech-to-text-transcription-in-the-cloud)
{.links-list}


# AWS Transcribe: Automating Speech-to-Text Transcription in the Cloud

Transcribing audio and video files is a time-consuming and error-prone task, which is only compounded when multiple speakers are involved. AWS Transcribe is a automatic speech recognition (ASR) service that makes it easy to transcribe audio files in a variety of languages in near real-time.

AWS Transcribe can be used to transcribe customer service calls, interviews, lectures, speeches, and more. The service can be accessed through the AWS Management Console, AWS Command Line Interface (CLI), and AWS SDK.

## Getting Started with AWS Transcribe

To get started with AWS Transcribe, create an account and sign in to the [AWS Management Console](https://console.aws.amazon.com/). Once you're signed in, navigate to the **Transcribe** service page and click **Create job**.

![](https://i.imgur.com/pkzL0bj.png)

On the next page, you'll be prompted to select the input file that you want to transcribe. The file must be stored in an Amazon Simple Storage Service (S3) bucket. You can also specify the language of the input file and whether to enable speaker recognition.

![](https://i.imgur.com/sTm7rTz.png)

Once you've selected the input file, click **Create job** to start the transcription process. The progress of the job can be monitored on the **Jobs** page.

![](https://i.imgur.com/GpqoNcu.png)

When the transcription job is complete, you can download the transcript in either plain text or JSON format.

![](https://i.imgur.com/Wql4Vfy.png)

## AWS Transcribe Pricing

AWS Transcribe is priced based on the length of the audio file being transcribed. The first 60 minutes of transcription is free, and thereafter it is $0.006 per minute. For example, transcribing a one-hour audio file would cost $0.36.

There is also a per-job fee of $0.0001, which is charged for each transcription job regardless of the length of the audio file.

## AWS Transcribe Limits

There are several limits that apply to AWS Transcribe jobs, including the following:

- The maximum size of an input file is 160 MB.
- The maximum length of an input file is 2 hours.
- The maximum number of jobs that can be queued is 1000.
- The maximum number of jobs that can be run concurrently is 100.

## Best Practices for Using AWS Transcribe

Here are some best practices to keep in mind when using AWS Transcribe:

- Make sure the audio quality is as high as possible to minimize errors in the transcription.
- Make sure the audio file is in a supported format, such as MP3, WAV, or FLAC.
- Transcribe short audio files (<10 minutes) to minimize transcription costs.
- Use speaker recognition to label different speakers in the transcript.

## Conclusion

AWS Transcribe is a powerful ASR service that can save you a lot of time and effort when transcribing audio files. Be sure to follow the best practices outlined in this article to get the most out of the service.