FROM ubuntu:latest

WORKDIR /app

RUN apt-get update && apt-get install -y \
    curl \
    gnupg \
    git \
    g++ \
    gcc \
    libgcc1 \
    libstdc++6 \
    linux-libc-dev \
    make \
    python3 \
    python3-pip \
    libtool \
    automake \
    autoconf \
    nasm \
    libjpeg-turbo8 \
    libjpeg-turbo8-dev \
    && rm -rf /var/lib/apt/lists/*

# Install Node.js 18.+
RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash - \
    && apt-get install -y nodejs \
    && node -v

# Install Yarn globally (version 3.4.1+ as required)
RUN npm install -g yarn@latest \
    && yarn --version

# Install wkhtmltopdf (for PDF generation)
RUN apt-get update && apt-get install -y wget \
    && wget https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6.1-3/wkhtmltox_0.12.6.1-3.jammy_amd64.deb \
    && apt-get install -y ./wkhtmltox_0.12.6.1-3.jammy_amd64.deb \
    && rm wkhtmltox_0.12.6.1-3.jammy_amd64.deb \
    && wkhtmltopdf --version

# Install libvips (for image processing)
RUN apt-get update && apt-get install -y \
    libvips42 \
    libvips-dev \
    && vips --version

RUN git clone https://github.com/AquilaCMS/AquilaCMS.git .

# Install AquilaCMS
RUN yarn install

#RUN cd apps/themes/default_theme_2 && yarn install && cd /app
RUN cd apps/themes/default_theme_2 \
    && yarn install --check-files \
    && yarn add next-translate-plugin \
    && ls -l node_modules/next-translate-plugin || echo "next-translate-plugin not installed" \
    && cat package.json || echo "No package.json found" \
    && cd /app

EXPOSE 8080

ENV NODE_ENV=production \
    PORT=8080 \
    # MONGODB_URI will be overridden at runtime to point to the MongoDB container
    MONGODB_URI=mongodb://mongo:27017/aquilacms \
    ADMIN_PREFIX=admin

CMD ["npm", "start"]