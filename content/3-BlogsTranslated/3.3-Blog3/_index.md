---
title: "Blog 3: S3 Files System"
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# Exploring S3 Files: Turning Amazon S3 Buckets into Local File Systems on AWS

*Original post link: [AWS Study Group Facebook Group](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2195923967839230)*


## Introduction

While researching storage solutions on AWS, I was quite impressed by an article introducing the **S3 Files** feature[cite: 5]. This is a novel solution that allows users to mount Amazon S3 Buckets directly into operating systems or applications as standard local drives/directories (File Systems)[cite: 5].

Instead of writing complex code using AWS SDKs or APIs to upload/download data, traditional applications can now read and write data directly to S3 via standard operating system file management commands[cite: 5].

---

## The Challenge

**Amazon S3** is a phenomenal Object Storage repository offering unlimited capacity at a low cost[cite: 5]. However, S3 is not a traditional File System[cite: 5]. 

Many legacy applications, data analytics tools, or automation scripts are designed strictly to read/write local files (*POSIX file interface*)[cite: 5]. To run these applications with S3, developers typically had to:
* Completely refactor the source code to integrate S3 APIs[cite: 5].
* Incur additional costs for intermediary services like AWS Storage Gateway[cite: 5].

This consumed time, inflated costs, and overcomplicated the system architecture[cite: 5].

---

## AWS's Approach

To optimally solve this problem, AWS launched **S3 Files** (powered by the open-source technology *Mountpoint for Amazon S3*)[cite: 5].

When this feature is activated, AWS creates an automatic translation "bridge": Your application writes files to a directory as usual, while S3 Files silently converts those commands into `GetObject` or `PutObject` APIs to push them straight to the S3 Bucket[cite: 5]. Consequently, you leverage a familiar file interface while fully enjoying the massive capacity and data durability of Amazon S3[cite: 5].

---

## Utilized AWS Services and Components

The operational architecture of this feature revolves around core components[cite: 5]:

| AWS Component | Architectural Role |
| :--- | :--- |
| **Amazon S3** | Acts as the origin storage vault (Simple Storage Service), containing all object data in the backend[cite: 5]. |
| **Mountpoint for Amazon S3** | The open-source translation client (S3 Files Client) installed on compute servers, responsible for converting file commands (POSIX) into S3 API calls[cite: 5]. |
| **Amazon EC2 / AWS Fargate** | The server or container environments running the actual applications – where the S3 directory is mounted for usage[cite: 5]. |
| **AWS IAM** | Controls security permissions (Identity and Access Management), ensuring servers only possess exact read/write clearance for authorized S3 directories[cite: 5]. |

This combination enables the system to operate with extreme high throughput, minimizing latency when processing large datasets without the need to manage complex storage hardware[cite: 5].

> *Figure 1. Architectural overview illustrating EC2 Instances connecting via TCP 2049 (NFS) to an S3 Files Mount Target to read/write directly into an S3 Bucket.*

![Architectural overview illustrating EC2 Instances connecting via TCP 2049 (NFS) to an S3 Files Mount Target](/images/3-BlogsTranslated/blog3-1.png)

---

## Practical Setup on the AWS Console

Setting up S3 Files is incredibly intuitive via the AWS management console:

1. **Initialize File System:** Users can start creating a file system directly from the Amazon S3 interface via Create, Mount, and Access steps.
> *Figure 2. The "Getting started with S3 Files" interface on the AWS Console detailing 3 foundational setup steps.*

2. **Configure Mount Targets:** These are internal network endpoints located within Virtual Private Cloud (VPC) Availability Zones (AZ).
> *Figure 3. The Mount targets management interface displaying internal IPs and the "Available" connection status allowing compute resources to access the file system.*

![Mount targets management interface displaying internal IPs and "Available" status](/images/3-BlogsTranslated/blog3-2.png)

---

## What I Learned

Through this article, I gained a much clearer understanding of how AWS blurs the lines between *Object Storage* and *File Storage*[cite: 5].

The most intriguing aspect is Mountpoint's performance optimization mechanism for large-scale sequential read/write tasks (such as Machine Learning datasets, Video processing, and Big Data)[cite: 5]. Rather than attempting to 100% emulate all complex features of a file system (which easily causes bottlenecks), AWS focuses on optimizing the most fundamental commands (Read, Write, List) to achieve maximum data transit speeds in and out of S3[cite: 5].

## Conclusion

The **S3 Files** feature is a highly practical and exceptionally valuable move by AWS to simplify application cloud migration[cite: 5]. By transforming S3 into a high-performance, cost-free local file system, AWS has saved engineers weeks of configuration coding[cite: 5].

This is a highly recommended solution for big data processing projects, AI/ML systems requiring continuous data feeds from S3, or any invoice/image storage system seeking to optimize operational costs without refactoring complex backend source codes[cite: 5].

* **Original Reference Source:** [AWS News Blog - Launching S3 Files](https://aws.amazon.com/vi/blogs/aws/launching-s3-files-making-s3-buckets-accessible-as-file-systems/)[cite: 5]