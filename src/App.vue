<template>
  <div id="app" class="digital-museum">
    <div class="hide">
      <h4>Sorry, this musuem is not accessible to your device. Open it on bigger devices. 1280px above.</h4>
    </div>
    <!-- Header Section -->
    <section class="museum-header">
      <h1>Welcome to Ocho-ocho Digital Museum</h1>
      <div class="h-description">
        <p>
          Discover the vibrant heart of Philippine popular culture. Our digital
          museum celebrates iconic moments, cherished stories, and timeless
          creativity that define our shared identity. Explore and relive the
          spirit of the Filipinos.
        </p>
      </div>
      <button class="header-btn" @click="scrollToNextSectionFromHeader">
        <svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" fill="currentColor" class="bi bi-chevron-double-down" viewBox="0 0 16 16">
          <path fill-rule="evenodd" d="M1.646 6.646a.5.5 0 0 1 .708 0L8 12.293l5.646-5.647a.5.5 0 0 1 .708.708l-6 6a.5.5 0 0 1-.708 0l-6-6a.5.5 0 0 1 0-.708"/>
          <path fill-rule="evenodd" d="M1.646 2.646a.5.5 0 0 1 .708 0L8 8.293l5.646-5.647a.5.5 0 0 1 .708.708l-6 6a.5.5 0 0 1-.708 0l-6-6a.5.5 0 0 1 0-.708"/>
        </svg>
      </button>
    </section>

    <!-- Main Title Section -->
    <section id="group-section" class="group-section">
      <div class="group-name">
          <h1>{{ groupName }}</h1>
          </div>
          <div class="group-members">
            <span v-for="(member, index) in groupMembers" :key="index">
              {{ member }}
            </span>
          </div>
    </section>

        <!-- Content Sections -->
        <section class="sections-container">
          <div
            v-for="(section, sectionIndex) in sections"
            :key="sectionIndex"
            class="museum-section"
            :style="{
              ...getBackgroundStyle(sectionIndex),
              minHeight: '100vh',
            }"
          >
      <h3>{{ section.title }}</h3>
      <p>{{ section.subintro }}</p>
      <div class="subsections">
        <div
          v-for="(subsection, subsectionIndex) in section.subsections"
          :key="subsectionIndex"
          class="subsection"
          :style="{ backgroundImage: `url(${subsection.image})` }"
          @click="openVirtualRoom(sectionIndex, subsectionIndex)"
        >
          <div class="subsection-title">{{ subsection.title }}</div>
          <button @click="openVirtualRoom(sectionIndex, subsectionIndex)">
            Check Out Room
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="30"
              height="30"
              fill="currentColor"
              class="bi bi-arrow-right-short"
              viewBox="0 0 16 16"
            >
              <path
                fill-rule="evenodd"
                d="M4 8a.5.5 0 0 1 .5-.5h5.793L8.146 5.354a.5.5 0 1 1 .708-.708l3 3a.5.5 0 0 1 0 .708l-3 3a.5.5 0 0 1-.708-.708L10.293 8.5H4.5A.5.5 0 0 1 4 8"
              />
            </svg>
          </button>
        </div>
      </div>
    </div>
    </section>

    <!-- Virtual Room Modal -->
    <div v-if="showModal" class="modal-overlay" @click.self="closeVirtualRoom">
      <div class="modal-content">
        <h3>{{ activeRoom.subtitle }}</h3>
        <p class="description">{{ activeRoom.description }}</p>
        <div class="images-container">
          <img
            v-for="(image, index) in activeRoom.images"
            :key="index"
            :src="image"
            alt="Subsection image"
            class="modal-image"
          />
        </div>
        <button class="close-modal" @click="closeVirtualRoom">Close</button>
      </div>
    </div>
  </div>

  

  
</template>



<script>
export default {
  data() {
    return {
      groupName: "Built and Presented by Teambangan",
      groupMembers: [
        "Jhan Philippe Moloa",
        "Maycaela Enguito",
        "Jether Daniel Torres",
      ],
      sections: [
        {
          title: "Key Events/Highlights",
          subintro: "This section covers major moments, including significant events, memorable releases, and milestones that have captured public interests.",
        },
        {
          title: "2000-2010",
          subsections: [
          {
              title: "Social",
              subtitle: "Friendster",
              image: require("@/assets/section 1/cover.png"),
              description:
                "Friendster, founded in 2002 by Jonathan Abrams, was among the pioneering social networking platforms, quickly amassing over 3 million users within months of its 2003 launch. Despite early success, it declined due to technical issues and competition from emerging platforms like MySpace and Facebook. In 2003, Friendster declined a $30 million acquisition offer from Google, a decision later viewed as a significant misstep. By 2008, the platform had over 115 million registered users, primarily in Asia. In 2009, it was acquired by Malaysia-based MOL Global for $26.4 million. Subsequently, in 2010, Facebook purchased Friendster's patents for $40 million.",
              images: [
              require("@/assets/section 1/63e303445030a75e83d8d0fe_friendster-min.webp"),

              ],
            },
            {
              title: "Economic",
              subtitle: "BPO growth and PH becomes BPO capital in 2010",
              image: require("@/assets/section 1/cover.png"),
              description: "Between 2000 and 2010, the Philippines experienced significant growth in its Business Process Outsourcing (BPO) industry, transforming into a global leader in the sector. In 2000, the BPO industry contributed a modest 0.075% to the country's Gross Domestic Product (GDP). By 2005, this figure had risen to 2.4%, with the Philippines capturing over 3% of the global BPO market. The industry's expansion was driven by factors such as a highly skilled, English-proficient workforce and competitive labor costs. In 2010, the Philippines was declared the world's BPO capital, employing approximately 525,000 individuals and generating $8.9 billion in revenue. This rapid growth was further supported by government initiatives, including the establishment of the Philippine Economic Zone Authority (PEZA), which offered tax incentives and streamlined processes to attract foreign investors. The BPO sector's expansion significantly contributed to the country's economic development during this period.",
              images: [
              require("@/assets/gallery 1/bgm1.jpg"),
              ],
            },
            {
              title: "Political",
              subtitle: "2000s violence by extremists",
              image: require("@/assets/section 1/cover.png"),
              description: "Between 2000 and 2010, the Philippines faced significant extremist violence, primarily from groups like Abu Sayyaf and the New People's Army (NPA). In 2000, Abu Sayyaf conducted high-profile kidnappings, including the abduction of 21 individuals from Malaysia's Sipadan Island, leading to a Philippine court sentencing 17 militants to life imprisonment in 2024. In 2001, the group seized hostages from the Dos Palmas resort in Palawan, resulting in the deaths of American missionary Martin Burnham and Filipino nurse Ediborah Yap during a rescue attempt in 2002. The NPA, designated a Foreign Terrorist Organization by the U.S. in 2002, continued its insurgency, with activities peaking in 2007, making it the largest group behind terrorist attacks in the country. These events underscored the persistent threat of extremist violence in the Philippines during the decade.",
              images: [
              require("@/assets/gallery 1/pal1.jpg"),
              ],
            },
            {
              title: "Cultural",
              subtitle: "Signing of the Philippine Cultural Heritage Act of 2009",
              image: require("@/assets/section 1/cover.png"),
              description: "In March 2010, the Philippines enacted Republic Act No. 10066, known as the National Cultural Heritage Act of 2009.  This legislation established the Philippine Registry of Cultural Property (PRECUP) to catalog and protect the nation's cultural assets. It also mandated the preservation of historic structures over 50 years old and strengthened the National Commission for Culture and the Arts (NCCA) along with its affiliated agencies. The Act was a response to incidents like the 2000 demolition of the Manila Jai Alai Building, aiming to prevent similar losses of cultural heritage.",
              images: [
              require("@/assets/gallery 1/pal1.jpg"),
              ],
            },
            {
              title: "Environmental ",
              subtitle: "Tropical Storm Ondoy 2009",
              image: require("@/assets/section 1/cover.png"),
              description: "On September 26, 2009, Tropical Storm Ondoy (internationally known as Ketsana) struck the Philippines, bringing an unprecedented 455 millimeters of rainfall within 24 hours, the highest recorded in 42 years. This deluge led to severe flooding across Metro Manila and surrounding provinces, with waters reaching up to 20 feet in some areas. The disaster affected over 9.3 million people, resulted in 956 fatalities, and caused extensive damage to infrastructure and agriculture. In response, the government declared a state of calamity in Metro Manila and 25 provinces, mobilizing resources for rescue and relief operations. The event highlighted the need for improved disaster preparedness and climate resilience in the Philippines.",
              images: [
              require("@/assets/gallery 1/pal1.jpg"),
              ],
            },
          ],
          
        },
        {
          title: "Present Time",
          subsections: [
          {
              title: "Social",
              subtitle: "Twitter becomes X after Elon Musk acquires it for $44 billion",
              image: require("@/assets/section 1/cover.png"),
              description:
                "In October 2022, Elon Musk acquired Twitter for $44 billion, initiating significant transformations within the platform. In July 2023, Musk rebranded Twitter as 'X' replacing its iconic bird logo with a stylized 'X' and redirecting the domain to x.com. This rebranding was part of Musk's vision to develop X into an 'everything app' akin to China's WeChat, integrating various services beyond social networking. The transition involved merging Twitter, Inc. into X Corp., effectively dissolving the original company structure. These changes have sparked discussions about the platform's future direction and its role in the social media landscape.",
              images: [
              require("@/assets/gallery 1/1_16a082288a7.1665217_806339932_16a082288a7_large.jpg"),
              ],
            },
            {
              title: "Economic",
              subtitle: "Philippines becomes worlds largest rice importer",
              image: require("@/assets/section 1/cover.png"),
              description: "In 2023, the Philippines became the world's largest rice importer, surpassing China with 3.8 million metric tons (MMT) of imports, projected to reach 4.1 MMT in 2024. (philstar.com) Despite being the seventh-largest rice producer globally, domestic production struggles to meet rising demand due to population growth and consumption. (business.inquirer.net) Vietnam remains the top supplier, emphasizing the Philippines' dependence on imported rice to sustain its food security.",
              images: [
              require("@/assets/gallery 1/bgm1.jpg"),
              ],
            },
            {
              title: "Political",
              subtitle: "Philippines 'war on drugs' killings",
              image: require("@/assets/section 1/cover.png"),
              description: "Between 2016 and 2022, the Philippines' 'war on drugs,'' initiated by President Rodrigo Duterte, resulted in over 6,000 reported deaths during police anti-drug operations, with human rights groups estimating the toll to be significantly higher. This campaign faced global criticism for alleged extrajudicial killings and lack of due process, sparking investigations by the International Criminal Court (ICC). Despite its controversies, the government defended the campaign as necessary for combating crime and illegal drugs, claiming it significantly reduced drug-related activities in the country.",
              images: [
              require("@/assets/gallery 1/pal1.jpg"),
              ],
            },
            {
              title: "Cultural",
              subtitle: "Celebration of Filipino Youtube Fanfest (YTFF)",
              image: require("@/assets/section 1/cover.png"),
              description: "The YouTube FanFest (YTFF) in the Philippines has become a significant celebration of the country's dynamic content creators. First held in Manila in 2015, the event brought together local and international YouTube stars for performances and fan interactions. It grew annually, featuring creators like Ranz Kyle, Niana Guerrero, and Mikey Bustos. In 2021, the event adapted to a virtual format due to the pandemic, showcasing Filipino talents such as SB19 and The Juans, underscoring the continued vibrancy of the Filipino YouTube community.",
              images: [
              require("@/assets/gallery 1/pal1.jpg"),
              ],
            },
            {
              title: "Environmental",
              subtitle: "Tropical Storm Kristine 2024",
              image: require("@/assets/section 1/cover.png"),
              description: "In October 2024, Severe Tropical Storm Kristine (Trami) struck Luzon, Philippines, causing widespread flooding, landslides, and affecting over 6 million people. The storm claimed at least 116 lives, left many missing, and resulted in ₱3.76 billion in agricultural damages. States of calamity were declared in hard-hit areas, highlighting the ongoing need for stronger disaster preparedness in the country.",
              images: [
              require("@/assets/gallery 1/pal1.jpg"),
              ],
            },
          ],
          
        },
        {
          title: "2030",
          subsections: [
          {
              title: "Social",
              subtitle: "A centralized hub for social media, moderated by AI, access to these platforms improve.",
              image: require("@/assets/section 1/cover.png"),
              description:
                "In the future, a centralized social media hub emerges, integrating major platforms for seamless access. AI moderation ensures safer, regulated spaces by detecting harmful content in real time. Improved connectivity broadens access, making social media more inclusive and efficient for users worldwide.",
              images: [
              require("@/assets/gallery 1/1_16a082288a7.1665217_806339932_16a082288a7_large.jpg"),
              ],
            },
            {
              title: "Economic",
              subtitle: "The need for importation of goods would be reduced after improvement of manufacturing capability of the Philippines.",
              image: require("@/assets/section 1/cover.png"),
              description: "In the future, the Philippines' improved manufacturing capabilities reduce the need for importing goods. Enhanced local production supports domestic demand, strengthens the economy, and fosters self-sufficiency, decreasing reliance on foreign markets.",
              images: [
              require("@/assets/gallery 1/bgm1.jpg"),
              ],
            },
            {
              title: "Political",
              subtitle: "Shifts in Philippine politics beyond 2030 focus on reform, digital governance, and inclusive leadership",
              image: require("@/assets/section 1/cover.png"),
              description: "After 2030, Philippine politics is expected to focus on federalism, digital governance, climate policies, and evolving regional autonomy in Bangsamoro. Leadership shifts toward younger, reform-driven figures will reflect changing voter demographics and a push for transparency and inclusive governance.",
              images: [
              require("@/assets/gallery 1/pal1.jpg"),
              ],
            },
            {
              title: "Cultural",
              subtitle: "Filipino Culture will be mostly be curated and presented through a digital medium",
              image: require("@/assets/section 1/cover.png"),
              description: "Filipino culture will be showcased and celebrated through a dynamic digital medium, blending tradition with innovation. This initiative will curate and present key aspects of Filipino heritage—arts, music, language, history, and values—through engaging, interactive, and visually compelling formats. By leveraging technology, it aims to preserve and promote the richness of Filipino identity to both local and global audiences, ensuring accessibility and inclusivity for future generations.",
              images: [
              require("@/assets/gallery 1/pal1.jpg"),
              ],
            },
            {
              title: "Environmental ",
              subtitle: "Multiple typhoons hit the Philippines in succession, floods will be more severe. Adaptability of Filipinos on these calamities remains the reelevant subject.",
              image: require("@/assets/section 1/cover.png"),
              description: "With multiple typhoons hitting the Philippines in succession and escalating flood severity, the resilience and adaptability of Filipinos in the face of these recurring calamities remain a critical focus. This highlights the urgent need for disaster preparedness, sustainable infrastructure, and community-driven solutions, while underscoring the enduring spirit and resourcefulness of the Filipino people.",
              images: [
              require("@/assets/gallery 1/pal1.jpg"),
              ],
            },
          ],
          
        },
        {
          title: "Aspects",
          subintro: "Here, we explore key features such as creative expressions, the role of technology, media platforms, and the stories that bring people together.",
        },
        {
          title: "Focus: Affect Senses & Feelings (2000-2010)",
          subsections: [
          {
              title: "The Wowowee Stampede",
              subtitle: "The Wowowee Stampede",
              image: require("@/assets/section 1/cover.png"),
              description:
                "The PhilSports Stadium Stampede (also referred to as the ULTRA stampede or the Wowowee stampede) was a crowd crush that occurred at the PhilSports Stadium (also known as the ULTRA) in Pasig, Metro Manila in the Philippines on February 4, 2006. It killed 73 people and injured about 400. About 30,000 people had gathered outside the stadium waiting to participate in the first anniversary episode of the former television variety show Wowowee.",
              images: [
              require("@/assets/gallery 1/1_16a082288a7.1665217_806339932_16a082288a7_large.jpg"),
              ],
            },
            {
              title: "Bagyong Milenyo",
              subtitle: "Bagyong Milenyo",
              image: require("@/assets/section 1/cover.png"),
              description: "Bagyong Milenyo, or Typhoon Xangsane, was a devastating tropical cyclone that struck the Philippines in   September 2006. It caused widespread destruction in Luzon, resulting in severe flooding, significant infrastructure damage, and loss of life, highlighting disaster preparedness challenges. Bagyong Milenyo (Typhoon Xangsane) struck the Philippines from September 25-29, 2006, causing extensive damage and 213 fatalities. It affected over 4 million people, particularly in Metro Manila, with losses totaling P6.6 billion. The typhoon highlighted safety issues with billboards, leading to their removal after fatalities caused by falling structures",
              images: [
              require("@/assets/gallery 1/bgm1.jpg"),
              ],
            },
            {
              title: "Philippine Airlines Flight 812",
              subtitle: "Philippine Airlines Flight 812",
              image: require("@/assets/section 1/cover.png"),
              description: "On May 25, 2000, Philippine Airlines Flight 812 was hijacked before landing in Manila. Armed with a gun and a grenade, the hijacker demanded valuables and attempted to escape via a homemade parachute. He died three days later when the parachute failed to deploy. Reginald Chua hijacked Philippine Airlines Flight 812, citing family abandonment as his motivation. Armed with a pistol and grenade, he demanded money before attempting to escape via parachute. His behavior during the incident raised concerns about his mental health, and his body was later found in Quezon.",
              images: [
              require("@/assets/gallery 1/pal1.jpg"),
              ],
            },
            {
              title: "Fiestas celebrated Filipino traditions through vibrant community events",
              subtitle: "Fiestas celebrated Filipino traditions through vibrant community events",
              image: require("@/assets/section 1/cover.png"),
              description: "On May 25, 2000, Philippine Airlines Flight 812 was hijacked before landing in Manila. Armed with a gun and a grenade, the hijacker demanded valuables and attempted to escape via a homemade parachute. He died three days later when the parachute failed to deploy. Reginald Chua hijacked Philippine Airlines Flight 812, citing family abandonment as his motivation. Armed with a pistol and grenade, he demanded money before attempting to escape via parachute. His behavior during the incident raised concerns about his mental health, and his body was later found in Quezon.",
              images: [
              require("@/assets/gallery 1/pal1.jpg"),
              ],
            },
            {
              title: "EDSA II",
              subtitle: "EDSA II",
              image: require("@/assets/section 1/cover.png"),
              description: "On May 25, 2000, Philippine Airlines Flight 812 was hijacked before landing in Manila. Armed with a gun and a grenade, the hijacker demanded valuables and attempted to escape via a homemade parachute. He died three days later when the parachute failed to deploy. Reginald Chua hijacked Philippine Airlines Flight 812, citing family abandonment as his motivation. Armed with a pistol and grenade, he demanded money before attempting to escape via parachute. His behavior during the incident raised concerns about his mental health, and his body was later found in Quezon.",
              images: [
              require("@/assets/gallery 1/pal1.jpg"),
              ],
            },
          ],
          
        },
        {
          title: "Affect Senses & Feelings (Present)",
          subsections: [
          {
              title: "The Wowowee Stampede",
              subtitle: "The Wowowee Stampede",
              image: require("@/assets/section 1/cover.png"),
              description:
                "The PhilSports Stadium Stampede (also referred to as the ULTRA stampede or the Wowowee stampede) was a crowd crush that occurred at the PhilSports Stadium (also known as the ULTRA) in Pasig, Metro Manila in the Philippines on February 4, 2006. It killed 73 people and injured about 400. About 30,000 people had gathered outside the stadium waiting to participate in the first anniversary episode of the former television variety show Wowowee.",
              images: [
              require("@/assets/gallery 1/1_16a082288a7.1665217_806339932_16a082288a7_large.jpg"),
              ],
            },
            {
              title: "Bagyong Milenyo",
              subtitle: "Bagyong Milenyo",
              image: require("@/assets/section 1/cover.png"),
              description: "Bagyong Milenyo, or Typhoon Xangsane, was a devastating tropical cyclone that struck the Philippines in   September 2006. It caused widespread destruction in Luzon, resulting in severe flooding, significant infrastructure damage, and loss of life, highlighting disaster preparedness challenges. Bagyong Milenyo (Typhoon Xangsane) struck the Philippines from September 25-29, 2006, causing extensive damage and 213 fatalities. It affected over 4 million people, particularly in Metro Manila, with losses totaling P6.6 billion. The typhoon highlighted safety issues with billboards, leading to their removal after fatalities caused by falling structures",
              images: [
              require("@/assets/gallery 1/bgm1.jpg"),
              ],
            },
            {
              title: "Philippine Airlines Flight 812",
              subtitle: "Philippine Airlines Flight 812",
              image: require("@/assets/section 1/cover.png"),
              description: "On May 25, 2000, Philippine Airlines Flight 812 was hijacked before landing in Manila. Armed with a gun and a grenade, the hijacker demanded valuables and attempted to escape via a homemade parachute. He died three days later when the parachute failed to deploy. Reginald Chua hijacked Philippine Airlines Flight 812, citing family abandonment as his motivation. Armed with a pistol and grenade, he demanded money before attempting to escape via parachute. His behavior during the incident raised concerns about his mental health, and his body was later found in Quezon.",
              images: [
              require("@/assets/gallery 1/pal1.jpg"),
              ],
            },
            {
              title: "Fiestas celebrated Filipino traditions through vibrant community events",
              subtitle: "Fiestas celebrated Filipino traditions through vibrant community events",
              image: require("@/assets/section 1/cover.png"),
              description: "On May 25, 2000, Philippine Airlines Flight 812 was hijacked before landing in Manila. Armed with a gun and a grenade, the hijacker demanded valuables and attempted to escape via a homemade parachute. He died three days later when the parachute failed to deploy. Reginald Chua hijacked Philippine Airlines Flight 812, citing family abandonment as his motivation. Armed with a pistol and grenade, he demanded money before attempting to escape via parachute. His behavior during the incident raised concerns about his mental health, and his body was later found in Quezon.",
              images: [
              require("@/assets/gallery 1/pal1.jpg"),
              ],
            },
            {
              title: "EDSA II",
              subtitle: "EDSA II",
              image: require("@/assets/section 1/cover.png"),
              description: "On May 25, 2000, Philippine Airlines Flight 812 was hijacked before landing in Manila. Armed with a gun and a grenade, the hijacker demanded valuables and attempted to escape via a homemade parachute. He died three days later when the parachute failed to deploy. Reginald Chua hijacked Philippine Airlines Flight 812, citing family abandonment as his motivation. Armed with a pistol and grenade, he demanded money before attempting to escape via parachute. His behavior during the incident raised concerns about his mental health, and his body was later found in Quezon.",
              images: [
              require("@/assets/gallery 1/pal1.jpg"),
              ],
            },
          ],
          
        },
        {
          title: "Body and Self Image",
          subsections: [
          {
              title: "Miss International 2005 Victory",
              image: require("@/assets/section 1/cover.png"),
              description:
              "In 2005, Precious Lara Quigaman’s Miss International win celebrated diverse Filipino beauty and sparked national pride. This victory shifted the focus from traditional beauty standards to a more inclusive view, highlighting intelligence and cultural identity, ultimately reshaping self-image in Philippine popular culture during the decade. Precious Lara’s Miss International win in 2005 influenced Philippine popular culture by promoting a broader definition of beauty. It encouraged self-acceptance and highlighted the importance of intelligence and cultural identity, leading to a more inclusive perspective on body image and self-worth during the 2000s.",
              images: [
                require("@/assets/gallery 2/2005-miss-international-winner-philippines-precious-lara-550nw-7828522b.jpg"),
                require("@/assets/gallery 2/845806bf9c531275af1bae331f79383a.jpg"),
                require("@/assets/gallery 2/1659413732_966318566_16_ent.png"),
              ],
            },
            {
              title: "Marian Rivera crowned as FHM Philippines' Sexiest Woman for 2008",
              image: require("@/assets/section 1/cover.png"),
              description: "Marian Rivera's rise to fame through her role in the hit show Marimar led to her crowning as FHM Philippines' Sexiest Woman in 2008. This victory not only celebrated her beauty but also brought the FHM awards into Philippine households, elevating the magazine's profile and influencing popular culture. Rivera's win showcased a blend of talent and attractiveness, encouraging greater acceptance of diverse beauty standards in the process. Marian Rivera's FHM win in 2008 influenced Philippine popular culture by reinforcing beauty ideals that emphasized physical appearance. While she inspired body positivity, it also risked promoting unrealistic standards among young fans, potentially impacting their self-image and leading to pressure to conform to these ideals.",
              images: [
                require("@/assets/gallery 2/mar1.jpg"),
                require("@/assets/gallery 2/mar2.jpg"),
                require("@/assets/gallery 2/mar3.webp"),
              ],
            },
            {
              title: "Emo Culture",
              image: require("@/assets/section 1/cover.png"),
              description: "Emo culture in the 2000s reshaped Philippine popular culture by promoting individuality and emotional expression. It influenced body image through distinctive fashion choices and encouraged discussions about mental health, allowing youth to embrace vulnerability and authenticity, ultimately transforming self-image and perceptions of beauty during the decade. Emo culture in the 2000s empowered Filipino youth by promoting individuality and personal expression. It encouraged them to embrace their unique identities and emotions, challenging societal norms and fostering a sense of belonging within a community that valued authenticity and diverse self-representation.",
              images: [
                require("@/assets/gallery 2/emo1.jpg"),
                require("@/assets/gallery 2/emo2.jpg"),
                require("@/assets/gallery 2/emo3.jpg"),
              ],
            },
            {
              title: "Marian Rivera crowned as FHM Philippines' Sexiest Woman for 2008",
              image: require("@/assets/section 1/cover.png"),
              description: "Marian Rivera's rise to fame through her role in the hit show Marimar led to her crowning as FHM Philippines' Sexiest Woman in 2008. This victory not only celebrated her beauty but also brought the FHM awards into Philippine households, elevating the magazine's profile and influencing popular culture. Rivera's win showcased a blend of talent and attractiveness, encouraging greater acceptance of diverse beauty standards in the process. Marian Rivera's FHM win in 2008 influenced Philippine popular culture by reinforcing beauty ideals that emphasized physical appearance. While she inspired body positivity, it also risked promoting unrealistic standards among young fans, potentially impacting their self-image and leading to pressure to conform to these ideals.",
              images: [
                require("@/assets/gallery 2/mar1.jpg"),
                require("@/assets/gallery 2/mar2.jpg"),
                require("@/assets/gallery 2/mar3.webp"),
              ],
            },
            {
              title: "Emo Culture",
              image: require("@/assets/section 1/cover.png"),
              description: "Emo culture in the 2000s reshaped Philippine popular culture by promoting individuality and emotional expression. It influenced body image through distinctive fashion choices and encouraged discussions about mental health, allowing youth to embrace vulnerability and authenticity, ultimately transforming self-image and perceptions of beauty during the decade. Emo culture in the 2000s empowered Filipino youth by promoting individuality and personal expression. It encouraged them to embrace their unique identities and emotions, challenging societal norms and fostering a sense of belonging within a community that valued authenticity and diverse self-representation.",
              images: [
                require("@/assets/gallery 2/emo1.jpg"),
                require("@/assets/gallery 2/emo2.jpg"),
                require("@/assets/gallery 2/emo3.jpg"),
              ],
            },
          ],
        },
        {
          title: "Performance",
          subsections: [
            {
              title: "Charice Pempengco on Oprah",
              image: require("@/assets/section 1/cover.png"),
              description:
                "Jake Cyrus, formerly known as Charice Pempengco, captivated audiences with her 2008 appearance on The Oprah Winfrey Show, showcasing Filipino talent on a global stage. Her powerful performances inspired national pride and encouraged aspiring artists, marking a significant moment in Philippine popular culture during the 2000s. Jake Cyrus's 2008 appearance on Oprah instilled a deep sense of pride among Filipino youth, as they saw one of their own achieving global recognition. This milestone inspired them to embrace their cultural identity and aspire to showcase their talents on an international stage.",
              images: [
              require("@/assets/gallery 5/char1.jpg"),
              require("@/assets/gallery 5/char2.jpg"),
              require("@/assets/gallery 5/char3.jpg"),
              ],
            },
            {
              title: "Local Films like Magnifico, One More Chance, & Tanging Yaman",
              image: require("@/assets/section 1/cover.png"),
              description: "The success of local films like Magnifico, One More Chance, and Tanging Yaman in the 2000s showcased powerful performances and emphasized family values. These movies resonated with audiences, fostering cultural pride and identity while elevating Philippine cinema as a significant force in the entertainment landscape during the decade. The success of local films in the 2000s instilled a sense of accomplishment as these award-winning movies garnered international recognition. This achievement fostered pride among Filipinos, motivating them to celebrate their cultural contributions and engage more deeply with their heritage.",
              images: [
              require("@/assets/gallery 5/fil1.webp"),
              require("@/assets/gallery 5/fil2.jpg"),
              require("@/assets/gallery 5/fil3.jpg"),
              ],
            },
            {
              title: "Sexbomb Girls - The Spageti Song",
              image: require("@/assets/section 1/cover.png"),
              description: "The Sexbomb Girls rose to fame through their appearances on Eat Bulaga in the 2000s, captivating audiences with their hit 'The Spaghetti Song'. Their catchy music, playful choreography, and humor celebrated fun and lightheartedness, significantly impacting Philippine popular culture and evolving standards of femininity.",
              images: [
              require("@/assets/gallery 5/spag1.jpg"),
              require("@/assets/gallery 5/spag2.jpg"),
              require("@/assets/gallery 5/spag3.webp"),
              ],
            },
            {
              title: "Local Films like Magnifico, One More Chance, & Tanging Yaman",
              image: require("@/assets/section 1/cover.png"),
              description: "The success of local films like Magnifico, One More Chance, and Tanging Yaman in the 2000s showcased powerful performances and emphasized family values. These movies resonated with audiences, fostering cultural pride and identity while elevating Philippine cinema as a significant force in the entertainment landscape during the decade. The success of local films in the 2000s instilled a sense of accomplishment as these award-winning movies garnered international recognition. This achievement fostered pride among Filipinos, motivating them to celebrate their cultural contributions and engage more deeply with their heritage.",
              images: [
              require("@/assets/gallery 5/fil1.webp"),
              require("@/assets/gallery 5/fil2.jpg"),
              require("@/assets/gallery 5/fil3.jpg"),
              ],
            },
            {
              title: "Sexbomb Girls - The Spageti Song",
              image: require("@/assets/section 1/cover.png"),
              description: "The Sexbomb Girls rose to fame through their appearances on Eat Bulaga in the 2000s, captivating audiences with their hit 'The Spaghetti Song'. Their catchy music, playful choreography, and humor celebrated fun and lightheartedness, significantly impacting Philippine popular culture and evolving standards of femininity.",
              images: [
              require("@/assets/gallery 5/spag1.jpg"),
              require("@/assets/gallery 5/spag2.jpg"),
              require("@/assets/gallery 5/spag3.webp"),
              ],
            },
          ],
        },
        {
          title: "Overall Observable Trends",
          subintro: "This section identifies broader patterns and recurring themes, highlighting how societal changes, technology, and audience preferences shape the landscape.",
        },
        {
          title: "Performance",
          subsections: [
            {
              title: "Charice Pempengco on Oprah",
              image: require("@/assets/section 1/cover.png"),
              description:
                "Jake Cyrus, formerly known as Charice Pempengco, captivated audiences with her 2008 appearance on The Oprah Winfrey Show, showcasing Filipino talent on a global stage. Her powerful performances inspired national pride and encouraged aspiring artists, marking a significant moment in Philippine popular culture during the 2000s. Jake Cyrus's 2008 appearance on Oprah instilled a deep sense of pride among Filipino youth, as they saw one of their own achieving global recognition. This milestone inspired them to embrace their cultural identity and aspire to showcase their talents on an international stage.",
              images: [
              require("@/assets/gallery 5/char1.jpg"),
              require("@/assets/gallery 5/char2.jpg"),
              require("@/assets/gallery 5/char3.jpg"),
              ],
            },
            {
              title: "Local Films like Magnifico, One More Chance, & Tanging Yaman",
              image: require("@/assets/section 1/cover.png"),
              description: "The success of local films like Magnifico, One More Chance, and Tanging Yaman in the 2000s showcased powerful performances and emphasized family values. These movies resonated with audiences, fostering cultural pride and identity while elevating Philippine cinema as a significant force in the entertainment landscape during the decade. The success of local films in the 2000s instilled a sense of accomplishment as these award-winning movies garnered international recognition. This achievement fostered pride among Filipinos, motivating them to celebrate their cultural contributions and engage more deeply with their heritage.",
              images: [
              require("@/assets/gallery 5/fil1.webp"),
              require("@/assets/gallery 5/fil2.jpg"),
              require("@/assets/gallery 5/fil3.jpg"),
              ],
            },
            {
              title: "Sexbomb Girls - The Spageti Song",
              image: require("@/assets/section 1/cover.png"),
              description: "The Sexbomb Girls rose to fame through their appearances on Eat Bulaga in the 2000s, captivating audiences with their hit 'The Spaghetti Song'. Their catchy music, playful choreography, and humor celebrated fun and lightheartedness, significantly impacting Philippine popular culture and evolving standards of femininity.",
              images: [
              require("@/assets/gallery 5/spag1.jpg"),
              require("@/assets/gallery 5/spag2.jpg"),
              require("@/assets/gallery 5/spag3.webp"),
              ],
            },
            {
              title: "Local Films like Magnifico, One More Chance, & Tanging Yaman",
              image: require("@/assets/section 1/cover.png"),
              description: "The success of local films like Magnifico, One More Chance, and Tanging Yaman in the 2000s showcased powerful performances and emphasized family values. These movies resonated with audiences, fostering cultural pride and identity while elevating Philippine cinema as a significant force in the entertainment landscape during the decade. The success of local films in the 2000s instilled a sense of accomplishment as these award-winning movies garnered international recognition. This achievement fostered pride among Filipinos, motivating them to celebrate their cultural contributions and engage more deeply with their heritage.",
              images: [
              require("@/assets/gallery 5/fil1.webp"),
              require("@/assets/gallery 5/fil2.jpg"),
              require("@/assets/gallery 5/fil3.jpg"),
              ],
            },
            {
              title: "Sexbomb Girls - The Spageti Song",
              image: require("@/assets/section 1/cover.png"),
              description: "The Sexbomb Girls rose to fame through their appearances on Eat Bulaga in the 2000s, captivating audiences with their hit 'The Spaghetti Song'. Their catchy music, playful choreography, and humor celebrated fun and lightheartedness, significantly impacting Philippine popular culture and evolving standards of femininity.",
              images: [
              require("@/assets/gallery 5/spag1.jpg"),
              require("@/assets/gallery 5/spag2.jpg"),
              require("@/assets/gallery 5/spag3.webp"),
              ],
            },
          ],
        },
        {
          title: "Thank you for visiting Ocho-ocho Digital Museum",
          subintro: "This section identifies broader patterns and recurring themes, highlighting how societal changes, technology, and audience preferences shape the landscape.",
        },
  
      ],
    
      
      showModal: false,
      activeRoom: {},
    };
  },
  mounted() {
    const appContainer = document.getElementById("app");
    appContainer.addEventListener("wheel", this.handleMouseWheel, {
      passive: false,
    });
  },
  beforeUnmount() {
    const appContainer = document.getElementById("app");
    appContainer.removeEventListener("wheel", this.handleMouseWheel);
  },
  methods: {
    getBackgroundStyle(index) {
      const backgrounds = [
        { type: 'background-color', value: "white" },
        { type: 'image', value: require("@/assets/bg-retro-3.png")},
        { type: 'image', value: require("@/assets/bg/6.png")}, 
        { type: 'image', value: require("@/assets/bg/5.png")},
        { type: 'background-color', value: "white" },
        { type: 'image', value: require("@/assets/bg/2.png")},
        { type: 'image', value: require("@/assets/bg/3.png")},
        { type: 'image', value: require("@/assets/bg/4.png")},
        { type: 'background-color', value: "white" },
        { type: 'image', value: require("@/assets/bg/5.png")},
       
      ];

      const bg = backgrounds[index % backgrounds.length]; // Cycle through backgrounds

      if (bg.type === 'color') {
        return { backgroundColor: bg.value }; // Return background color style
      } else if (bg.type === 'image') {
        return {
          backgroundImage: `url(${bg.value})`,
          backgroundSize: 'cover',
          backgroundRepeat: 'no-repeat',
          backgroundPosition: 'center',
        }; // Return background image style
      }

      return { backgroundColor: '#FFFFFF' }; // Default fallback
    },
    scrollToNextSectionFromHeader() {
      const target = document.getElementById("group-section"); // Ensure ID matches
      if (target) {
        target.scrollIntoView({ behavior: "smooth" }); // Smooth scrolling
      }
    },
    openVirtualRoom(sectionIndex, subsectionIndex) {
      this.activeRoom =
        this.sections[sectionIndex].subsections[subsectionIndex];
      this.showModal = true;
    },
    closeVirtualRoom() {
      this.showModal = false;
      this.activeRoom = {};
    },
    handleMouseWheel(event) {
      event.preventDefault(); // Prevent default scroll behavior
      const scrollAmount = event.deltaY > 0 ? 100 : -100; // Adjust scroll speed
      window.scrollBy({
        top: scrollAmount,
        behavior: "smooth", // Smooth scrolling
      });
    },
  },

};
</script>


<style src="./styles.css"></style>
